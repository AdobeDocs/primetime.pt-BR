---
title: Lógica de domínio anônimo
description: Lógica de domínio anônimo
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Lógica de domínio anônimo{#anonymous-domain-logic}

## Lógica de registro de domínio {#section_C91DCD49D7D44570AF98C2D7B8A283F9}

A implementação de referência aplica a seguinte lógica para registro de domínio anônimo:

1. Analise o nome de domínio do URL da solicitação.
1. Procure o nome de domínio no `DomainServerInfo` tabela.
1. Se não conseguir localizar uma entrada, insira uma entrada na tabela.

   Os valores padrão são:

   * `authentication is not required`
   * `no membership maximum`

   Se a autenticação for necessária para o domínio solicitado, verifique se há um token de autenticação válido na solicitação. Se o Namespace de autenticação estiver especificado no banco de dados, o token deverá corresponder ao Namespace de autenticação especificado.
1. Se a autenticação for necessária, mas um token de autenticação válido não estiver disponível, retornar um erro `DOM_AUTHENTICATION_REQUIRED (503)`.
1. Verifique se o dispositivo está registrado com o domínio:

   1. Procure o nome de domínio no `DomainMembership` tabela.
   1. Compare o GUID do computador localizado com o GUID do computador na solicitação.
   1. Se esta for uma nova máquina, adicione uma entrada na `DomainMembership` tabela.
   1. Se for um novo dispositivo e `Max Membership` valor foi atingido, erro de retorno `DOM_LIMIT_REACHED (502)`.

1. Pesquisar todas as chaves de domínio para este domínio no `DomainKeys` tabela:

   1. Se `DomainServerInfo` indica que as chaves precisam ser sobrepostas, gere um novo par de chaves.
   1. Salve o par de chaves no `DomainKeys` tabela, com uma versão da chave que é um número maior que a chave existente mais alta.
   1. Redefina o `Key Rollover Required` sinalizador em `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

## Lógica de cancelamento de registro de domínio {#section_C968BBFCBFAB4510A903D169F38C9FCE}

A implementação de referência aplica a seguinte lógica para o cancelamento de registro de domínio anônimo:

1. Analise o nome de domínio do URL da solicitação.
1. Procure o nome de domínio solicitado no `DomainServerInfo` tabela.
1. Se a autenticação for necessária para o domínio solicitado, verifique se há um token de autenticação válido na solicitação.

   O token também deve corresponder ao Namespace de autenticação especificado no banco de dados.
1. Pesquise o nome de domínio e o GUID do computador no `DomainMembership` tabela.

   Se você não puder localizar uma entrada correspondente, retornará um erro `DEREG_DENIED (401)`.

1. Se essa não for uma solicitação de visualização, exclua a entrada de `DomainMembership`e em `DomainServerInfo`, defina o `Key Rollover Required` sinalizador.

Como um grande número de computadores pode ingressar no domínio, você não pode simplesmente corresponder à ID do computador. Em vez disso, a GUID de máquina aleatória atribuída à máquina durante a individualização é aplicada.
