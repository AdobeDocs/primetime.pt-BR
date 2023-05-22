---
title: Domínios baseados em identidade
description: Domínios baseados em identidade
copied-description: true
exl-id: de7b6c8a-5227-4679-933a-3278921903d7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Domínios baseados em identidade {#identity-based-domains}

Nesse caso de uso, cada usuário autenticado tem seu próprio domínio e um determinado número de dispositivos tem permissão para ingressar no domínio. Para usar esse tipo de domínio com a implementação de referência, crie uma política especificando que o registro de domínio é necessário. Especifique o host e a porta do servidor para o URL do servidor de domínio e especifique que a autenticação de nome de usuário/senha é necessária.

A implementação de referência implementa a seguinte lógica para o registro de domínio:

1. Determine o nome de domínio a ser atribuído a esse usuário. O nome do domínio será * `namequalifier:username`* extraído do token de autenticação. Se não houver um token de autenticação, retorne o erro DOM_AUTHENTICATION_REQUIRED (503).
1. Pesquisar o nome de domínio no `DomainServerInfo` tabela. Se uma entrada não for encontrada, insira uma entrada na tabela (os valores padrão são autenticação necessária, associação máxima de domínio=5).
1. Verifique se o dispositivo já foi registrado com o domínio:

   1. Pesquise o nome de domínio no `UserDomainMembership` tabela. Para cada ID de máquina encontrada, compare com a ID de máquina na solicitação. Se esta for uma nova máquina, adicione uma entrada à `UserDomainMembership` tabela. Em seguida, localize os registros correspondentes em `UserDomainRefCount` tabela. Se não existir uma entrada para esse GUID de computador, adicione um registro.

   1. Se for um novo dispositivo e a Associação máxima já tiver sido atingida, retornará o erro DOM_LIMIT_REACHED (502).

1. Pesquisar todas as chaves do domínio na tabela DomainKeys.

   1. Se `DomainServerInfo` indica que as chaves precisam ser sobrepostas, gere um novo par de chaves e salve-o no `DomainKeys` (com a versão da chave uma superior à chave existente mais alta) e redefina o sinalizador &quot;Sobreposição de chave necessária&quot; no `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

A implementação de referência implementa a seguinte lógica para o cancelamento do registro de domínio:

1. Determine o nome de domínio a ser atribuído a esse usuário. O nome do domínio será *namequalifier:nome de usuário* extraído do token de autenticação. Se não houver um token de autenticação, retorne o erro DOM_AUTHENTICATION_REQUIRED (503).
1. Pesquisar o nome de domínio solicitado na `DomainServerInfo` tabela.
1. Pesquisar o nome de domínio no `UserDomainMembership` tabela. Para cada ID de máquina encontrada, compare com a ID de máquina na solicitação. Localize a entrada correspondente no `UserDomainRefCount` tabela. Se uma entrada correspondente não for encontrada, retornará o erro DEREG_DENIED (401).

1. Se essa não for uma solicitação de visualização, exclua a entrada de `UserDomainRefCount` tabela. Se não houver mais entradas nessa tabela para a máquina, exclua a entrada de `UserDomainMembership` e defina o sinalizador &quot;Sobreposição de chave necessária&quot; no `DomainServerInfo`.

Nesse caso de uso, cada usuário tem permissão para registrar um pequeno número de máquinas, para que possamos usar a ID completa da máquina e a variável `matches()` para contar com precisão as máquinas. No entanto, como o usuário pode se registrar várias vezes nessa máquina (por meio de vários aplicativos do AIR ou Players em navegadores diferentes), o servidor também precisa manter uma contagem de referência, para que o cancelamento de registro possa ser contado com precisão. O cancelamento do registro não pode ser considerado concluído, até que todos os tokens de domínio no computador sejam renderizados.
