---
title: Lógica de registro de domínio com base na identidade
description: Lógica de registro de domínio com base na identidade
copied-description: true
exl-id: 6e391fce-00b4-45cf-b785-3b0ec734a11e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Lógica de registro de domínio com base na identidade{#identity-based-domain-registration-logic}

## Lógica de registro de domínio {#section_149C247458954877AF158B4A09A8526B}

A implementação de referência aplica a seguinte lógica para o registro de domínio com base em identidade:

1. Determine o nome de domínio a ser atribuído a um usuário designado.

   O nome de domínio ( `namequalifier:username`) é extraído do token de autenticação. Se um token não estiver disponível, um erro será lançado.
1. Procure o nome de domínio no `DomainServerInfo` tabela.

   Se nenhuma entrada for encontrada, insira uma entrada. Os valores padrão são:

   * `authentication required`
   * `max domain membership=5`

   .

1. Para verificar se o dispositivo foi registrado no domínio:

   1. Procure o `domainname` no `UserDomainMembership` tabela:

      1. Para cada ID de máquina localizada, compare a ID com a ID da máquina na solicitação.
      1. Se esta for uma nova máquina, adicione uma entrada à `UserDomainMembership` tabela.
      1. Pesquisar os registros correspondentes em `UserDomainRefCount` tabela.
      1. Se não existir uma entrada para esse GUID de computador, adicione um registro.
   1. Se for um novo dispositivo, e a variável `Max Membership` valor foi atingido, retorne o erro.


1. Pesquisar todas as chaves de domínio para este domínio no `DomainKeys` tabela:

   1. Se `DomainServerInfo` indica que as chaves precisam ser sobrepostas, gere um novo par de chaves,
   1. Salve o par no `DomainKeys` tabela, com uma versão de chave superior à maior chave existente.
   1. Redefina o `Key Rollover Required` sinalizador em `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

## Lógica de cancelamento de registro de domínio {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

A implementação de referência aplica a seguinte lógica para o cancelamento do registro de domínio com base em identidade:

1. Determine o nome de domínio a ser atribuído a esse usuário.

   O nome do domínio é `namequalifier:username`, que é extraído do token de autenticação. Se nenhum token estiver disponível, retornar o erro `DOM_AUTHENTICATION_REQUIRED (503)` ocorre.
1. Procure o nome de domínio solicitado no `DomainServerInfo` tabela.
1. Procure o nome de domínio no `UserDomainMembership` tabela.
1. Compare cada ID de máquina encontrada com a ID de máquina na solicitação.
1. Localize a entrada correspondente no campo `UserDomainRefCount` tabela.

   Se uma entrada correspondente não for localizada, retornará o erro .

1. Se essa não for uma solicitação de visualização, exclua a entrada da variável `UserDomainRefCount` tabela.
1. Se não houver entradas adicionais nessa tabela para a máquina, exclua a entrada de `UserDomainMembership` e defina o [!DNL Key Rollover Required] sinalizador no `DomainServerInfo` propriedade.

Cada usuário pode registrar um pequeno número de computadores para que você possa usar a ID completa do computador e `matches()` método para contar computadores. Como um usuário pode se registrar várias vezes, por meio de vários aplicativos ou players do AIR em navegadores diferentes, o servidor precisa manter uma contagem de referência para que o cancelamento do registro também possa ser contado.

>[!NOTE]
>
>O cancelamento do registro não é concluído até que todos os tokens de domínio no computador sejam entregues.
