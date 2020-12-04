---
seo-title: Domínios Anônimos
title: Domínios Anônimos
uuid: ee29ae4d-65b2-48de-b441-18c8cf55de32
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Domínios Anônimos {#anonymous-domains}

Nesse caso de uso, um grande número de dispositivos pertence a um único domínio, e a autenticação pode não ser necessária. Para usar esse tipo de domínio com a implementação de referência, crie a política que especifica que o registro de domínio é obrigatório. Especifique o URL do servidor de domínio como `https:// host:port/flashaccess/domainserver/domainname/` e especifique a autenticação anônima.

A implementação de referência implementa a seguinte lógica para o registro de domínio:

1. Analise o nome do domínio do URL de solicitação.
1. Pesquise o nome do domínio na tabela `DomainServerInfo`. Se uma entrada não for encontrada, insira uma entrada na tabela (valores padrão: autenticação não é obrigatória e nenhuma associação é máxima).
1. Se a autenticação for necessária para o domínio solicitado, verifique se um token de autenticação válido foi incluído na solicitação e corresponda à Namespace de autenticação, se especificado no banco de dados.

   1. Se a autenticação for necessária, mas nenhum token de autenticação válido tiver sido fornecido, retorne o erro `DOM_AUTHENTICATION_REQUIRED (503)`.

1. Verifique se o dispositivo já se registrou no domínio:

   1. Pesquise o nome do domínio na tabela `DomainMembership`. Para cada GUID de computador encontrado, compare com o GUID do computador na solicitação. Se esta for uma nova máquina, adicione uma entrada à tabela `DomainMembership`.

   1. Se for um novo dispositivo e a associação máxima já tiver sido atingida, retorne o erro `DOM_LIMIT_REACHED (502)`.

1. Pesquise todas as chaves de domínio para este domínio na tabela `DomainKeys`.

   1. Se `DomainServerInfo` indicar que as teclas precisam ser sobrepostas, gere um novo par de chaves, salve-o na tabela `DomainKeys` (com a versão principal uma superior à chave existente mais alta) e redefina o sinalizador `Key Rollover Required` em `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

A implementação de referência implementa a seguinte lógica para o cancelamento do registro do domínio:

1. Analise o nome do domínio do URL de solicitação.
1. Pesquise o nome de domínio solicitado na tabela `DomainServerInfo`.
1. Se a autenticação for necessária para o domínio solicitado, verifique se um token de autenticação válido foi incluído na solicitação e corresponda à Namespace de autenticação, se especificado no banco de dados.
1. Pesquise o nome do domínio e o GUID da máquina na tabela `DomainMembership`. Se uma entrada correspondente não for encontrada, retorne o erro `DEREG_DENIED (401)`.

1. Se esta não for uma solicitação de pré-visualização, exclua a entrada de `DomainMembership` e defina o sinalizador `Key Rollover Required` em `DomainServerInfo`.

Nesse caso de uso, como um grande número de máquinas pode ingressar no domínio, não é possível corresponder completamente à ID da máquina. Em vez disso, o GUID de máquina aleatório atribuído à máquina durante a individualização é usado.
