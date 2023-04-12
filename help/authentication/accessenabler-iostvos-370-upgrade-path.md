---
title: Caminho de atualização do AccessEnabler iOS/tvOS 3.7.0
description: Caminho de atualização do AccessEnabler iOS/tvOS 3.7.0
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Caminho de atualização do AccessEnabler iOS/tvOS 3.7.0 {#accessenabler-iostvos-370-upgrade-path}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

Alterações no armazenamento do chaveiro do [nova versão do AccessEnabler 3.7.0](/help/authentication/authn-rn-ios-tvos-370.md) são incompatíveis com a implementação de armazenamento do chaveiro a partir da versão do AccessEnabler anterior à 3.7.0.

O caminho de atualização de um aplicativo que adota a nova versão 3.7.0 do AccessEnabler migrará todos os tokens das versões anteriores do armazenamento do Keychain. Portanto, usuários finais **não deve ter perda de sessões de autenticação/autorização** durante o processo de atualização da estrutura do AccessEnabler.

## Limitações conhecidas

Algumas limitações, descritas abaixo, podem ser encontradas pelos implementadores.


1. O SSO regular (Adobe) não funcionará entre um aplicativo usando o AccessEnabler versão 3.7.0 e um aplicativo usando versões do AccessEnabler inferiores a 3.7.0, mesmo para aplicativos desenvolvidos pelo mesmo fornecedor.

   - **Importante:**
      - O SSO (System Level, nível de sistema) não será afetado!
      - O SSO regular (Adobe) continuará a funcionar se ambos os aplicativos forem desenvolvidos pelo mesmo fornecedor e se as versões do AccessEnabler forem inferiores a 3.7.0!
      - O SSO regular (Adobe) funcionará se ambos os aplicativos forem desenvolvidos pelo mesmo fornecedor e usar o AccessEnabler versão 3.7.0!

1. Na situação de rebaixar um aplicativo usando a versão 3.7.0 do AccessEnabler para uma versão inferior do AccessEnabler, os novos tokens gerados não serão migrados. Portanto, os usuários finais podem sofrer a perda das sessões de autenticação/autorização, sem esperar isso.

   - **Importante:**
      - Os usuários finais autenticados por meio do SSO no nível do sistema (Apple) não serão afetados!
      - Os usuários finais que já foram autenticados antes da atualização para o novo aplicativo usando o AccessEnabler versão 3.7.0 não serão afetados!

1. Na situação de rebaixar um aplicativo usando a versão 3.7.0 do AccessEnabler para uma versão inferior do AccessEnabler, os tokens excluídos não serão reconhecidos. Portanto, os usuários finais podem experimentar a presença de sessões de autenticação/autorização, sem esperá-la.
