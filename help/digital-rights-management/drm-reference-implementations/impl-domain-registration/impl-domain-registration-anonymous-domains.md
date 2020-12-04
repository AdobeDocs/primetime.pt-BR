---
description: nulo
seo-description: nulo
seo-title: Lógica de domínio anônima
title: Lógica de domínio anônima
uuid: bd0e8e51-27dc-4ccf-b285-a80c2ab9e260
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Lógica de domínio anônima{#anonymous-domain-logic}

## Lógica de registro do domínio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

A implementação de referência aplica a seguinte lógica para o registro de domínio anônimo:

1. Analise o nome do domínio do URL de solicitação.
1. Procure o nome do domínio na tabela `DomainServerInfo`.
1. Se não conseguir localizar uma entrada, insira uma entrada na tabela.

   Os valores padrão são:

   * `authentication is not required`
   * `no membership maximum`

   Se a autenticação for necessária para o domínio solicitado, verifique se há um token de autenticação válido na solicitação. Se a Namespace de autenticação for especificada no banco de dados, o token deverá corresponder à Namespace de autenticação especificada.
1. Se a autenticação for necessária, mas um token de autenticação válido não estiver disponível, retorne o erro `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Verifique se o dispositivo está registrado no domínio:

   1. Procure o nome do domínio na tabela `DomainMembership`.
   1. Compare o GUID da máquina que você localizar com o GUID da máquina na solicitação.
   1. Se esta for uma nova máquina, adicione uma entrada na tabela `DomainMembership`.
   1. Se for um novo dispositivo e o valor `Max Membership` tiver sido atingido, retorne o erro `DOM_LIMIT_REACHED (502)`.

1. Procure todas as chaves de domínio para este domínio na tabela `DomainKeys`:

   1. Se `DomainServerInfo` indicar que as teclas precisam ser revertidas, gere um novo par de teclas.
   1. Salve o par de chaves na tabela `DomainKeys`, com uma versão de chave que seja um número superior à chave mais alta existente.
   1. Redefina o sinalizador `Key Rollover Required` em `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

## Lógica de cancelamento de registro do domínio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

A implementação de referência aplica a seguinte lógica para o cancelamento do registro de domínio anônimo:

1. Analise o nome do domínio do URL de solicitação.
1. Procure o nome de domínio solicitado na tabela `DomainServerInfo`.
1. Se a autenticação for necessária para o domínio solicitado, verifique se há um token de autenticação válido na solicitação.

   O token também deve corresponder à Namespace Auth especificada no banco de dados.
1. Procure o nome do domínio e o GUID da máquina na tabela `DomainMembership`.

   Se não conseguir localizar uma entrada correspondente, retorne o erro `DEREG_DENIED (401)`.

1. Se esta não for uma solicitação de pré-visualização, exclua a entrada de `DomainMembership` e, em `DomainServerInfo`, defina o sinalizador `Key Rollover Required`.

Como um grande número de máquinas pode ingressar no domínio, você não pode simplesmente corresponder à ID da máquina. Em vez disso, o GUID de máquina aleatório atribuído ao computador durante a individualização é aplicado.
