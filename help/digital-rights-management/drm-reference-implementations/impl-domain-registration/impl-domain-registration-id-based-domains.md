---
title: Lógica de registro de domínio baseada em identidade
description: Lógica de registro de domínio baseada em identidade
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Lógica de registro de domínio baseada em identidade{#identity-based-domain-registration-logic}

## Lógica de registro de domínio {#section_149C247458954877AF158B4A09A8526B}

A implementação de referência aplica a seguinte lógica para o registro de domínio baseado na identidade:

1. Determine o nome de domínio a ser atribuído a um usuário designado.

   O nome de domínio ( `namequalifier:username`) é extraído do token de autenticação. Se um token não estiver disponível, o erro será lançado.
1. Procure o nome de domínio na tabela `DomainServerInfo`.

   Se nenhuma entrada for encontrada, insira uma entrada. Os valores padrão são:

   * `authentication required`
   * `max domain membership=5`

   .

1. Para verificar se o dispositivo foi registrado no domínio:

   1. Procure `domainname` na tabela `UserDomainMembership`:

      1. Para cada ID de máquina localizada, compare a ID com a ID do computador na solicitação.
      1. Se esta for uma nova máquina, adicione uma entrada à tabela `UserDomainMembership`.
      1. Procure os registros correspondentes na tabela `UserDomainRefCount`.
      1. Se não existir uma entrada para este GUID de computador, adicione um registro.
   1. Se for um novo dispositivo e o valor `Max Membership` tiver sido atingido, retorne o erro .


1. Procure todas as chaves de domínio para este domínio na tabela `DomainKeys`:

   1. Se `DomainServerInfo` indicar que as chaves precisam ser revertidas, gere um novo par de chaves,
   1. Salve o par na tabela `DomainKeys`, com uma versão principal que seja uma superior à chave mais alta existente.
   1. Redefina o sinalizador `Key Rollover Required` em `DomainServerInfo`.

   1. Para cada chave de domínio, gere uma credencial de domínio.

## Lógica de cancelamento de registro do domínio {#section_78AFA63D8F744BE6BCA10A51B4FCBA22}

A implementação de referência aplica a seguinte lógica para o cancelamento do registro do domínio baseado na identidade:

1. Determine o nome de domínio a ser atribuído a este usuário.

   O nome de domínio é `namequalifier:username`, que é extraído do token de autenticação. Se nenhum token estiver disponível, o erro de retorno `DOM_AUTHENTICATION_REQUIRED (503)` ocorrerá.
1. Procure o nome de domínio solicitado na tabela `DomainServerInfo`.
1. Procure o nome de domínio na tabela `UserDomainMembership`.
1. Compare cada ID de máquina encontrada com a ID de máquina na solicitação.
1. Localize a entrada correspondente na tabela `UserDomainRefCount`.

   Se uma entrada correspondente não estiver localizada, retorne o erro .

1. Se esta não for uma solicitação de visualização, exclua a entrada da tabela `UserDomainRefCount`.
1. Se não houver entradas adicionais nessa tabela para a máquina, exclua a entrada de `UserDomainMembership` e defina o sinalizador [!DNL Key Rollover Required] na propriedade `DomainServerInfo`.

Cada usuário pode registrar um pequeno número de máquinas, de modo que você pode usar a ID completa da máquina e o método `matches()` para contar máquinas. Como um usuário pode registrar várias vezes, por meio de vários aplicativos AIR ou Players em navegadores diferentes, o servidor precisa manter uma contagem de referência para que o cancelamento de registro também possa ser contado.

>[!NOTE]
>
>O cancelamento de registro não é concluído até que todos os tokens de domínio no computador sejam renderizados.

