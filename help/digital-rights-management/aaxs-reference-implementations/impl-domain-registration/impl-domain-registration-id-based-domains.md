---
seo-title: Domínios baseados em identidade
title: Domínios baseados em identidade
uuid: 34cad19b-1adb-4e0c-ac59-50632f6988f7
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Domínios baseados em identidade {#identity-based-domains}

Nesse caso de uso, cada usuário autenticado tem seu próprio domínio, e um determinado número de dispositivos tem permissão para entrar no domínio. Para usar esse tipo de domínio com a implementação de referência, é necessário criar uma política que especifique o registro de domínio. Especifique o host e a porta do servidor para o URL do servidor de domínio e especifique se a autenticação de nome de usuário/senha é necessária.

A implementação de referência implementa a seguinte lógica para o registro de domínio:

1. Determine o nome do domínio a ser atribuído a este usuário. O nome do domínio será * `namequalifier:username`* extraído do token de autenticação. Se não houver token de autenticação, retorne o erro DOM_AUTHENTICATION_REQUIRED (503).
1. Pesquise o nome do domínio na tabela `DomainServerInfo`. Se uma entrada não for encontrada, insira uma entrada na tabela (os valores padrão são autenticação obrigatória, associação máxima de domínio=5).
1. Verifique se o dispositivo já se registrou no domínio:

   1. Pesquise o nome do domínio na tabela `UserDomainMembership`. Para cada ID de máquina encontrada, compare com a ID de máquina na solicitação. Se esta for uma nova máquina, adicione uma entrada à tabela `UserDomainMembership`. Em seguida, localize os registros correspondentes na tabela `UserDomainRefCount`. Se não existir uma entrada para este GUID de computador, adicione um registro.

   1. Se for um novo dispositivo e a associação máxima já tiver sido atingida, retorne o erro DOM_LIMIT_REACHED (502).

1. Pesquise todas as chaves de domínio para este domínio na tabela DomainKeys.

   1. Se `DomainServerInfo` indicar que as chaves precisam ser sobrepostas, gere um novo par de chaves, salve-o na tabela `DomainKeys` (com a versão principal uma superior à chave existente mais alta) e redefina o sinalizador &quot;Chave de sobreposição exigida&quot; em `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

A implementação de referência implementa a seguinte lógica para o cancelamento do registro do domínio:

1. Determine o nome do domínio a ser atribuído a este usuário. O nome do domínio será *namequalifier:username* extraído do token de autenticação. Se não houver token de autenticação, retorne o erro DOM_AUTHENTICATION_REQUIRED (503).
1. Pesquise o nome de domínio solicitado na tabela `DomainServerInfo`.
1. Pesquise o nome do domínio na tabela `UserDomainMembership`. Para cada ID de máquina encontrada, compare com a ID de máquina na solicitação. Encontre a entrada correspondente na tabela `UserDomainRefCount`. Se uma entrada correspondente não for encontrada, retorne o erro DEREG_DENIED (401).

1. Se esta não for uma solicitação de pré-visualização, exclua a entrada da tabela `UserDomainRefCount`. Se não houver mais entradas nessa tabela para a máquina, exclua a entrada de `UserDomainMembership` e defina o sinalizador &quot;Chave de sobreposição obrigatória&quot; em `DomainServerInfo`.

Nesse caso de uso, cada usuário tem permissão para registrar um pequeno número de máquinas, portanto, podemos usar a ID completa do computador e o método `matches()` para contar com precisão as máquinas. Entretanto, como o usuário pode se registrar várias vezes nesta máquina (por meio de vários aplicativos AIR ou Players em navegadores diferentes), o servidor também precisa manter uma contagem de referência, para que o cancelamento de registro possa ser contado com precisão. O cancelamento de registro não pode ser considerado concluído até que todos os tokens de domínio no computador sejam renderizados.
