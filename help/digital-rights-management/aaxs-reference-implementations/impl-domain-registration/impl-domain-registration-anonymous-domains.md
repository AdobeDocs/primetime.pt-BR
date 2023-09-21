---
title: Domínios Anônimos
description: Domínios Anônimos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Domínios Anônimos {#anonymous-domains}

Nesse caso de uso, um grande número de dispositivos pertence a um único domínio e a autenticação pode não ser necessária. Para usar esse tipo de domínio com a implementação de referência, crie a política especificando que o registro do domínio é necessário. Especifique o URL do servidor de domínio como `https:// host:port/flashaccess/domainserver/domainname/` e especificar autenticação anônima.

A implementação de referência implementa a seguinte lógica para o registro de domínio:

1. Analise o nome de domínio do URL da solicitação.
1. Pesquisar o nome de domínio no `DomainServerInfo` tabela. Se uma entrada não for encontrada, insira uma entrada na tabela (valores padrão: autenticação não é necessária e nenhuma associação máxima).
1. Se a autenticação for necessária para o domínio solicitado, verifique se um token de autenticação válido foi incluído na solicitação e se ele corresponde ao Namespace de autenticação, se especificado no banco de dados.

   1. Se a autenticação for necessária, mas nenhum token de autenticação válido for fornecido, retornar um erro `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Verifique se o dispositivo já foi registrado com o domínio:

   1. Pesquisar o nome de domínio no `DomainMembership` tabela. Para cada GUID de máquina encontrado, compare com o GUID de máquina na solicitação. Se esta for uma nova máquina, adicione uma entrada à `DomainMembership` tabela.

   1. Se for um novo dispositivo e a Associação Máxima já tiver sido atingida, retornará um erro `DOM_LIMIT_REACHED (502)`.

1. Pesquisar todas as chaves de domínio para este domínio no `DomainKeys` tabela.

   1. Se `DomainServerInfo` indica que as chaves precisam ser sobrepostas, gere um novo par de chaves e salve-o no `DomainKeys` tabela (com a versão da chave uma superior à chave existente mais alta) e redefina a `Key Rollover Required` sinalizador em `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

A implementação de referência implementa a seguinte lógica para o cancelamento do registro de domínio:

1. Analise o nome de domínio do URL da solicitação.
1. Pesquisar o nome de domínio solicitado na `DomainServerInfo` tabela.
1. Se a autenticação for necessária para o domínio solicitado, verifique se um token de autenticação válido foi incluído na solicitação e se ele corresponde ao Namespace de autenticação, se especificado no banco de dados.
1. Pesquise o nome de domínio e a GUID do computador no `DomainMembership` tabela. Se uma entrada correspondente não for encontrada, retorna o erro `DEREG_DENIED (401)`.

1. Se essa não for uma solicitação de visualização, exclua a entrada de `DomainMembership` e defina o `Key Rollover Required` sinalizador em `DomainServerInfo`.

Nesse caso de uso, como um grande número de máquinas pode ingressar no domínio, não é possível corresponder completamente à ID da máquina. Em vez disso, a GUID de máquina aleatória atribuída à máquina durante a individualização é usada.
