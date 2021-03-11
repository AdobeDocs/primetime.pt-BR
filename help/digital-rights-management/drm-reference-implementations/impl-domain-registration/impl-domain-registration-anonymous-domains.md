---
title: Lógica de domínio anônima
description: Lógica de domínio anônima
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Lógica de domínio anônima{#anonymous-domain-logic}

## Lógica de registro de domínio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

A implementação de referência aplica a seguinte lógica para o registro de domínio anônimo:

1. Analise o nome de domínio do URL da solicitação.
1. Procure o nome de domínio na tabela `DomainServerInfo`.
1. Se não for possível localizar uma entrada, insira uma entrada na tabela.

   Os valores padrão são:

   * `authentication is not required`
   * `no membership maximum`

   Se a autenticação for necessária para o domínio solicitado, verifique se um token de autenticação válido está na solicitação. Se o Namespace de Autenticação for especificado no banco de dados, o token deverá corresponder ao Namespace de Autenticação especificado.
1. Se a autenticação for necessária, mas um token de autenticação válido não estiver disponível, retorne o erro `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Verifique se o dispositivo está registrado com o domínio:

   1. Procure o nome de domínio na tabela `DomainMembership`.
   1. Compare o GUID da máquina que você localiza com o GUID da máquina na solicitação.
   1. Se esta for uma nova máquina, adicione uma entrada na tabela `DomainMembership`.
   1. Se for um novo dispositivo e o valor `Max Membership` for atingido, retorne o erro `DOM_LIMIT_REACHED (502)`.

1. Procure todas as chaves de domínio para este domínio na tabela `DomainKeys`:

   1. Se `DomainServerInfo` indicar que as chaves precisam ser revertidas, gere um novo par de chaves.
   1. Salve o par de chaves na tabela `DomainKeys`, com uma versão de chave que é um número maior que a chave mais alta existente.
   1. Redefina o sinalizador `Key Rollover Required` em `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

## Lógica de cancelamento de registro do domínio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

A implementação de referência aplica a seguinte lógica para o cancelamento de registro de domínio anônimo:

1. Analise o nome de domínio do URL da solicitação.
1. Procure o nome de domínio solicitado na tabela `DomainServerInfo`.
1. Se a autenticação for necessária para o domínio solicitado, verifique se um token de autenticação válido está na solicitação.

   O token também deve corresponder ao Namespace de Autenticação especificado no banco de dados.
1. Procure o nome de domínio e o GUID do computador na tabela `DomainMembership`.

   Se não conseguir localizar uma entrada correspondente, retorne o erro `DEREG_DENIED (401)`.

1. Se esta não for uma solicitação de visualização, exclua a entrada de `DomainMembership` e, em `DomainServerInfo`, defina o sinalizador `Key Rollover Required`.

Como um grande número de máquinas pode ingressar no domínio, você não pode simplesmente corresponder à ID do computador. Em vez disso, o GUID de máquina aleatório atribuído à máquina durante a individualização é aplicado.
