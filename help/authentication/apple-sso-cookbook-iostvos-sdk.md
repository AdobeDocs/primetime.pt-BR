---
title: Guia SSO do Apple (SDK do iOS/tvOS)
description: Guia SSO do Apple (SDK do iOS/tvOS)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 0%

---



# Guia SSO do Apple (SDK do iOS/tvOS) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#Introduction}

O SDK iOS/tvOS do Adobe Primetime Authentication AccessEnabler pode oferecer suporte à autenticação de logon único (SSO) da plataforma para usuários finais de aplicativos clientes em execução no iOS, iPadOS ou tvOS por meio do que chamamos de fluxo de trabalho SSO do Apple.

Observe que este documento atua como uma extensão para a documentação de SDK do AccessEnabler iOS/tvOS existente, que pode ser encontrada [here](/help/authentication/iostvos-sdk-api-reference.md).

</br>

## Guia {#Cookbook}

Para se beneficiar da experiência do usuário do Apple SSO, um aplicativo precisaria integrar o SDK do AccessEnabler iOS/tvOS e seguir a sequência de dicas apresentadas abaixo.

</br>

### Pré-requisitos {#Prerequisites}

</br>

#### Permissão

>[!TIP]
>
> **<u>Dica Pro:</u>** Para ter acesso às informações de assinatura do usuário, o usuário deve conceder ao aplicativo permissão para continuar, de modo semelhante ao acesso à câmera ou ao microfone do dispositivo. Essa permissão deve ser solicitada por aplicativo e o dispositivo salvará a seleção do usuário. Lembre-se de que o usuário pode alterar sua decisão acessando as configurações do aplicativo (acesso de permissão do provedor de TV) ou a seção de *`Settings -> TV Provider`* no iOS/iPadOS ou *`Settings -> Accounts -> TV Provider`* no tvOS.

>[!TIP]
>
> **<u>Dica Pro:</u>** Recomendamos solicitar a permissão do usuário quando o aplicativo entrar no estado de primeiro plano, mas é apenas uma sugestão, pois o aplicativo pode verificar [permissão de acesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) as informações de assinatura do usuário em qualquer ponto antes de exigir autenticação do usuário. Além disso, as APIs do SDK do AccessEnabler iOS/tvOS solicitarão automaticamente a permissão do usuário quando necessário.

>[!TIP]
>
> **<u>Dica Pro:</u>** Caso o usuário não conceda acesso a suas informações de assinatura ou caso a comunicação com a estrutura da conta do assinante de vídeo falhe, o SDK do AccessEnabler iOS/tvOS voltará ao fluxo de autenticação regular.

>[!TIP]
>
> **<u>Dica Pro:</u>** Recomendamos incentivar os usuários que se recusam a conceder permissão de acesso às informações de assinatura explicando os benefícios da experiência do usuário de Logon único (SSO). Lembre-se de que o usuário pode alterar sua decisão acessando as configurações do aplicativo (acesso de permissão do provedor de TV) ou a seção de *`Settings -> TV Provider`* no iOS/iPadOS ou *`Settings -> Accounts -> TV Provider`* no tvOS.


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                   // Do nothing.
                
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                   // Incentivize users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from Settings -> TV Provider on iOS/iPadOS or Settings -> Accounts -> TV Provider on tvOS.
                   ...
                }
    }
    ... 
```

</br>

#### Retornos de chamada

>[!TIP]
>
> **<u>Dica Pro:</u>** Implemente a seguinte lista de [retornos de chamada](/help/authentication/iostvos-sdk-api-reference.md) que são específicas ao workflow SSO do Apple.

- [*currentTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog) - Retorno de chamada acionado quando o seletor MVPD do Apple for aberto.
- [*dismissTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog) - Retorno de chamada disparado quando o seletor MVPD do Apple será fechado.

</br>

#### Relatório de erros

>[!TIP]
>
> **<u>Dica Pro:</u>** Implemente a seguinte lista de [códigos de erro avançados](/help/authentication/error-reporting.md) que são específicas ao workflow SSO do Apple.

- ***N003*** - O usuário selecionou a opção &quot;Outro provedor de TV&quot; no seletor MVPD do Apple.
- ***N004*** - O usuário selecionou um Provedor de TV no seletor MVPD do Apple, que não é suportado (integração ou Logon único desativado) pelo solicitante atual.
- ***N005*** - O usuário decidiu cancelar o seletor MVPD normal ou o seletor MVPD do Apple.
- ***VSA403*** - A permissão do Provedor de TV do usuário é negada para o aplicativo.
- ***VSA404*** - A permissão do Provedor de TV do usuário é indeterminada para o aplicativo.
- ***VSA503*** - Falha na solicitação de metadados da conta do assinante de vídeo, mais contexto é fornecido em *message* campo.
- ***AAPL / APPL_ERROR*** - Falha na solicitação de metadados da conta do assinante de vídeo, mais contexto é fornecido em *detalhes* campo. 

</br>

### Autenticação {#Authentication}

>[!TIP]
>
> **<u>Dica:</u>** Siga as etapas abaixo para a implementação do iOS/iPadOS/tvOS.

1. O pedido teria de [initialize](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) o SDK do AccessEnabler iOS/tvOS.
1. O pedido teria de [definir o identificador atual do solicitante](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

   **Importante:** Essa segunda etapa pode acionar uma [código de erro avançado](/help/authentication/error-reporting.md) que é específico para o workflow SSO do Apple, no caso **um dos seguintes é verdadeiro**:

   - ***VSA403*** - A permissão do Provedor de TV do usuário é negada para o aplicativo.
   - ***VSA404*** - A permissão do Provedor de TV do usuário é indeterminada para o aplicativo.
   - ***APPL*** - A comunicação entre o SDK do AccessEnabler iOS/tvOS e a estrutura de conta do assinante de vídeo encontrou um erro.

   Essa segunda etapa tentaria trocar silenciosamente o perfil SSO do Apple por um token de autenticação do Adobe, caso **todas as informações acima são falsas** e **todos os itens a seguir são verdadeiros**:

   - A permissão Provedor de TV do usuário é concedida para o aplicativo.
   - O usuário está conectado à conta do Provedor de TV no nível do sistema do dispositivo.
   - O SDK do AccessEnabler iOS/tvOS recebeu o identificador do provedor de TV do usuário da estrutura de conta do assinante de vídeo.
   - A integração do Provedor de TV do usuário com o aplicativo é habilitada por meio do Painel TVE da Adobe Primetime.
   - O Logon Único do Provedor de TV do usuário com o aplicativo é ativado por meio do Painel TVE do Adobe Primetime.
   - O Provedor de TV do usuário não é degradado pelo Painel TVE da Adobe Primetime.
   - O SDK do AccessEnabler iOS/tvOS recebeu a resposta SAML do provedor de TV do usuário a partir da estrutura de conta do assinante de vídeo.

   **<u>Dica Pro:</u>** Essa segunda etapa não acionará outros retornos de chamada além do [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) retorno de chamada, já que a autenticação não foi iniciada explicitamente pelo aplicativo.

1. O pedido teria de [verifique o status de autenticação](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

   **Importante:** Essa terceira etapa pode acionar uma [código de erro avançado](/help/authentication/error-reporting.md) que é específico para o workflow SSO do Apple, no caso **um dos seguintes é verdadeiro**:

   - ***VSA403** - O usuário está conectado à conta do Provedor de TV no nível do sistema do dispositivo, mas a permissão do Provedor de TV do usuário é negada para o aplicativo.
   - ***VSA404** - O usuário está conectado à conta do Provedor de TV no nível do sistema do dispositivo, mas a permissão do Provedor de TV do usuário é indeterminada para o aplicativo.
   - ***APPL\_ERROR** - O usuário está conectado à conta do provedor de TV no nível do sistema do dispositivo, mas a comunicação entre o SDK do AccessEnabler iOS/tvOS e a estrutura de conta do assinante de vídeo encontrou um erro.

   **Importante:** Essa terceira etapa acionará a variável [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) retorno de chamada com *status* igual a 0, em caso **um dos seguintes é verdadeiro**:

   - O usuário não está conectado à conta do Provedor de TV no nível do sistema do dispositivo ou por meio de um fluxo de autenticação regular.
   - O usuário está conectado à conta do Provedor de TV no nível do sistema do dispositivo ou por meio de um fluxo de autenticação regular, mas o TTL do token de autenticação do Provedor de TV do usuário foi transmitido.
   - O usuário faz logon na conta do Provedor de TV no nível do sistema do dispositivo ou por meio de um fluxo de autenticação regular, mas a integração do Provedor de TV do usuário com o aplicativo é desabilitada por meio do Painel Adobe Primetime TVE.
   - O usuário está conectado à conta do Provedor de TV no nível do sistema do dispositivo, mas o Logon Único do Provedor de TV do usuário com o aplicativo está desativado por meio do Painel TVE da Adobe Primetime.
   - O usuário está conectado à conta do Provedor de TV no nível do sistema do dispositivo, mas a permissão do Provedor de TV do usuário é negada para o aplicativo.
   - O usuário está conectado à conta do Provedor de TV no nível do sistema do dispositivo, mas a permissão do Provedor de TV do usuário é indeterminada para o aplicativo.
   - O usuário está conectado à conta do provedor de TV no nível do sistema do dispositivo, mas a comunicação entre o SDK do AccessEnabler iOS/tvOS e a estrutura de conta do assinante de vídeo encontrou um erro.

   **Importante:** Essa terceira etapa acionará a variável [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) retorno de chamada com *status* igual a 1, em caso **todas as informações acima são falsas.**


1. O pedido teria de [inicializar a autenticação](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) caso a verificação de status de autenticação anterior tenha disparado a variável [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) retorno de chamada com *status* igual a 0.

   **<u>Dica Pro:</u>** Implemente uma das seguintes API do SDK do AccessEnabler iOS/tvOS [getAuthentication](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) ou [getAuthentication:filter](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter).

   **Importante:** Esta quarta etapa pode acionar uma [código de erro avançado](/help/authentication/error-reporting.md) que é específico para o workflow SSO do Apple, no caso **um dos seguintes é verdadeiro**:

   - ***VSA403*** - A permissão do Provedor de TV do usuário é negada para o aplicativo.
   - ***VSA404*** - A permissão do Provedor de TV do usuário é indeterminada para o aplicativo.
   - ***VSA503*** - A comunicação entre o SDK do AccessEnabler iOS/tvOS e a estrutura de conta do assinante de vídeo encontrou um erro.
   - ***N003*** - O usuário selecionou a opção &quot;Outro provedor de TV&quot; no seletor MVPD do Apple.
   - ***N004*** - O usuário selecionou um Provedor de TV no seletor MVPD do Apple, que não é suportado (integração ou Logon único desativado) pelo solicitante atual.
   - ***N005*** - O usuário decidiu cancelar o seletor MVPD normal ou o seletor MVPD do Apple.

   **Importante:** Essa quarta etapa seria fallback para o fluxo de autenticação regular, acionando o [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) retorno de chamada e **one** do [códigos de erro avançados](/help/authentication/error-reporting.md), caso **um dos acima é verdadeiro**. 

   **Importante:** Essa quarta etapa seria fallback para o fluxo de autenticação regular, acionando o [navigateToUrl](/help/authentication/iostvos-sdk-api-reference.md#nav2url) ou [navigateToUrl:useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) retorno de chamada e **nenhum** do [códigos de erro avançados](/help/authentication/error-reporting.md), caso o usuário tenha selecionado um provedor de TV, que não é compatível com o Apple SSO, mas está presente no seletor do Apple MVPD.

   **<u>Dica Pro:</u>** O SDK do AccessEnabler iOS/tvOS chama silenciosamente a função [setSeletedProvder](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) Caso o usuário tenha selecionado um provedor de TV, que não é compatível com o Apple SSO, mas está presente no seletor MVPD do Apple.

   **Importante:** Essa quarta etapa tentaria trocar silenciosamente o perfil SSO do Apple por um token de autenticação do Adobe, caso **todas as informações acima são falsas** e **todos os itens a seguir são verdadeiros**:

   - A permissão Provedor de TV do usuário é concedida para o aplicativo.
   - O usuário está conectado/faz logon na conta do Provedor de TV no nível do sistema do dispositivo.
   - O SDK do AccessEnabler iOS/tvOS recebeu o identificador do provedor de TV do usuário da estrutura de conta do assinante de vídeo.
   - A integração do Provedor de TV do usuário com o aplicativo é habilitada por meio do Painel TVE da Adobe Primetime.
   - O Logon Único do Provedor de TV do usuário com o aplicativo é ativado por meio do Painel TVE do Adobe Primetime.
   - O Provedor de TV do usuário não é degradado pelo Painel TVE da Adobe Primetime.
   - O SDK do AccessEnabler iOS/tvOS recebeu a resposta SAML do provedor de TV do usuário a partir da estrutura de conta do assinante de vídeo.


 

>**<u>Dica Pro:</u>** Esta quarta etapa acionará a [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) retorno de chamada, independentemente de *status* , já que a autenticação foi iniciada explicitamente pelo aplicativo.


</br>

### Metadados {#Metadata}

O aplicativo tem a opção de determinar se a autenticação aconteceu como resultado de um logon por meio do SSO da plataforma ou não, usando o &quot;*tokenSource&quot;* [metadados do usuário](/help/authentication/iostvos-sdk-api-reference.md#getMeta) API do SDK do AccessEnabler iOS/tvOS.

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### Logout {#Logout}

O [Conta de assinante de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) O framework não fornece uma API para fazer logoff programaticamente de pessoas que entraram em sua conta do provedor de TV no nível do sistema do dispositivo. Portanto, para que o logout tenha efeito total, o usuário final teria que fazer logoff explicitamente de *`Settings -> TV Provider`* no iOS/iPadOS ou *`Settings -> Accounts -> TV Provider`* no tvOS. A outra opção que o usuário teria é retirar a permissão para acessar as informações de assinatura do usuário na seção de configurações específicas do aplicativo (acesso de permissão do Provedor de TV).

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio do SDK do AccessEnabler iOS/tvOS [logout](/help/authentication/iostvos-sdk-api-reference.md#logout) API.


>[!TIP]
>
> **<u>Dica Pro:</u>** Siga as etapas abaixo para as implementações de tvOS.

- O pedido teria de [iniciar o logout](/help/authentication/iostvos-sdk-api-reference.md#logout) no SDK do AccessEnabler iOS/tvOS. Isso não facilitaria a limpeza da sessão no lado do MVPD.
- O aplicativo teria que instruir/solicitar que o usuário saia explicitamente do *`Settings -> Accounts -> TV Provider`* somente no tvOS, caso [*VSA203* o código de status é acionado](/help/authentication/error-reporting.md).

>[!TIP]
>
> **<u>Dica Pro:</u>** Siga as etapas abaixo para as implementações do iOS/iPadOS.

- O pedido teria de [iniciar o logout](/help/authentication/iostvos-sdk-api-reference.md#logout) no SDK do AccessEnabler iOS/tvOS. Isso facilitaria a limpeza da sessão no lado do MVPD.
- O aplicativo teria que instruir/solicitar que o usuário saia explicitamente do *`Settings -> TV Provider`* no iOS/iPadOS somente no caso [*VSA203* o código de status é acionado](/help/authentication/error-reporting.md).


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
