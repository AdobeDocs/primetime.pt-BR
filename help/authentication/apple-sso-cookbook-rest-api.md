---
title: Guia SSO do Apple (REST API)
description: Guia SSO do Apple (REST API)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# Guia SSO do Apple (REST API) {#apple-sso-cookbook-rest-api}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#Introduction}

A API REST de autenticação da Adobe Primetime pode ser compatível com a autenticação de logon único (SSO) da plataforma para usuários finais de aplicativos clientes em execução no iOS, iPadOS ou tvOS por meio do fluxo de trabalho de SSO da Apple.

Observe que este documento atua como uma extensão para a documentação da API REST existente, que pode ser encontrada [here](/help/authentication/rest-api-reference.md).

</br>

## Livros {#Cookbooks}

Para se beneficiar da experiência do usuário do SSO Apple, um aplicativo precisaria integrar o [Conta de assinante de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) A estrutura desenvolvida pela Apple, embora com relação à comunicação da API REST de autenticação da Adobe Primetime, ela precisaria seguir a sequência de dicas apresentadas abaixo.

</br>

### Autenticação {#Authentication}

- [Existe um token de autenticação Adobe válido?](#Is_there_a_valid_Adobe_authentication_token)
- [O usuário está conectado via Platform SSO?](#Is_the_user_logged_in_via_Platform_SSO)
- [Buscar configuração do Adobe](#Fetch_Adobe_configuration)
- [Iniciar o fluxo de trabalho SSO da plataforma com a configuração de Adobe](#Initiate_Platform_SSO_workflow_with_Adobe_config)
- [O logon do usuário é bem-sucedido?](#Is_user_login_successful)
- [Obter uma solicitação de perfil do Adobe para o MVPD selecionado](#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD)
- [Encaminhe a solicitação do Adobe para o Platform SSO para obter o perfil](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile)
- [Troque o perfil de SSO da plataforma por um token de autenticação de Adobe](#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token)
- [O token de Adobe é gerado com êxito?](#Is_Adobe_token_generated_successfully)
- [Iniciar fluxo de trabalho de autenticação de segunda tela](#Initiate_second_screen_authentication_workflow)
- [Prosseguir com os fluxos de autorização](#Proceed_with_authorization_flows)

 

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/qu/platform-sso.jpeg)

</br>

#### Etapa: &quot;Existe um token de autenticação Adobe válido?&quot; {#Is_there_a_valid_Adobe_authentication_token}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio do [Autenticação Adobe Primetime](/help/authentication/check-authentication-token.md) serviço.

</br>

#### Etapa: &quot;O usuário está conectado via Platform SSO?&quot; {#Is_the_user_logged_in_via_Platform_SSO}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio do [Conta de assinante de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) estrutura.

- O aplicativo teria que verificar [permissão de acesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) as informações de assinatura do usuário e continue somente se o usuário tiver permitido.
- O pedido deverá apresentar um pedido [solicitação](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) para informações de conta de assinante.
- O aplicativo teria que aguardar e processar a variável [metadados](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) informações.

 

>[!TIP]
>
> **<u>Dica Pro:</u>** Siga o trecho do código e preste atenção nos comentários.

```swift
...
let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();

videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
            switch (accessStatus) {
            // The user allows the application to access subscription information.
            case VSAccountAccessStatus.granted:
                    // Construct the request for subscriber account information.
                    let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();

                    // This is actually the SAML Issuer not the channel ID.
                    vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAccountProviderIdentifier = true;
                    
                    // This is the subscription account information needed at this step.
                    vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                    
                    // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                    vsaMetadataRequest.isInterruptionAllowed = false;
                    
                    // Submit the request for subscriber account information - accountProviderIdentifier.
                    videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in        
                        if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                            // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                            // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                            ...
                            // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                            // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                            ...
                            // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                            // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                            ...
                            // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                            ...
                            // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                            ...
                        } else {
                            // The user is not authenticated at platform level, continue with the "Fetch Adobe configuration" step.
                            ...
                        }
                    }
        
            // The user has not yet made a choice or does not allow the application to access subscription information.
            default:
                // Fallback to regular authentication workflow.
                ...
            }
}
...  
```

</br>

#### Etapa: &quot;Buscar configuração do Adobe&quot; {#Fetch_Adobe_configuration}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio do [Autenticação Adobe Primetime](/help/authentication/provide-mvpd-list.md) serviço.


>[!TIP]
>
> **<u>Dica Pro:</u>** Esteja ciente das propriedades do MVPD: *`enablePlatformServices`*, *`boardingStatus`*, *`displayInPlatformPicker`*, *`platformMappingId`*, *`requiredMetadataFields`* e preste mais atenção aos comentários apresentados em trechos de código de outras etapas.

</br>

#### Etapa &quot;Iniciar fluxo de trabalho SSO da plataforma com configuração de Adobe&quot; {#Initiate_Platform_SSO_workflow_with_Adobe_config}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio do [Conta de assinante de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) estrutura.

- O aplicativo teria que verificar [permissão de acesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) as informações de assinatura do usuário e continue somente se o usuário tiver permitido.
- O pedido deverá fornecer um [delegate](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanagerdelegate) para o VSAccountManager.
- O pedido deverá apresentar um pedido [solicitação](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) para informações de conta de assinante.
- O aplicativo teria que aguardar e processar a variável [metadados](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) informações.

 

>[!TIP]
>
> **<u>Dica Pro:</u>** Siga o trecho do código e preste atenção nos comentários.


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    // This must be a class implementing the VSAccountManagerDelegate protocol.
    let videoSubscriberAccountManagerDelegate: VideoSubscriberAccountManagerDelegate = VideoSubscriberAccountManagerDelegate();
    
    videoSubscriberAccountManager.delegate = videoSubscriberAccountManagerDelegate;
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is the subscription account information needed at this step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to prompt the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = true;
                        
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to filter the TV providers from the Apple picker.
                        vsaMetadataRequest.supportedAccountProviderIdentifiers = supportedAccountProviderIdentifiers;
    
                        // This can be computed from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service response in order to sort the TV providers from the Apple picker.
                        if #available(iOS 11.0, tvOS 11, *) {
                            vsaMetadataRequest.featuredAccountProviderIdentifiers = featuredAccountProviderIdentifiers;
                        }
                        
                        // Submit the request for subscriber account information - accountProviderIdentifier.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in                        
                            // This represents the checks for the "Is user login successful?" step.
                            if (vsaMetadata != nil && vsaMetadata!.accountProviderIdentifier != nil) {
                                // The vsaMetadata!.authenticationExpirationDate will contain the expiration date for current authentication session.
                                // The vsaMetadata!.authenticationExpirationDate should be compared against current date.
                                ...
                                // The vsaMetadata!.accountProviderIdentifier will contain the provider identifier as it is known for the platform configuration.
                                // The vsaMetadata!.accountProviderIdentifier represents the platformMappingId in terms of Adobe Primetime Authentication configuration.
                                ...
                                // The application must determine the MVPD id property value based on the platformMappingId property value obtained above.
                                // The application must use the MVPD id further in its communication with Adobe Primetime Authentication services.
                                ...
                                // Continue with the "Obtain a profile request from Adobe for the selected MVPD" step.
                                ...
                                // Continue with the "Forward the Adobe request to Platform SSO to obtain the profile" step.
                                ...
                            } else {
                                // The user is not authenticated at platform level.
                                if (vsaError != nil) {
                                    // The application can check to see if the user selected a provider which is present in Apple picker, but the provider is not onboarded in platform SSO.
                                    if let error: NSError = (vsaError! as NSError), error.code == 1, let appleMsoId = error.userInfo["VSErrorInfoKeyUnsupportedProviderIdentifier"] as! String? {
                                        var mvpd: Mvpd? = nil;
    
                                        // The requestor.mvpds must be computed during the "Fetch Adobe configuration" step. 
                                        for provider in requestor.mvpds {
                                            if provider.platformMappingId == appleMsoId {
                                                mvpd = provider;
                                                break;
                                            }
                                        }
                                        
                                        if mvpd != nil {
                                            // Continue with the "Initiate second screen authentcation workflow" step, but you can skip prompting the user with your MVPD picker and use the mvpd selection, therefore creating a better UX.
                                            ...
                                        } else {
                                            // Continue with the "Initiate second screen authentcation workflow" step.
                                            ...
                                        }
                                    } else {
                                        // Continue with the "Initiate second screen authentcation workflow" step.
                                        ...
                                    }
                                } else {
                                    // Continue with the "Initiate second screen authentcation workflow" step.
                                    ...
                                }
                            }
                        }
            
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### Etapa: &quot;O logon do usuário é bem-sucedido?&quot; {#Is_user_login_successful}

>[!TIP]
>
> **<u>Dica Pro:</u>** Esteja ciente do trecho de código do [&quot;Iniciar o fluxo de trabalho SSO da plataforma com a configuração de Adobe&quot;](#Initiate_Platform_SSO_workflow_with_Adobe_config) etapa. O logon do usuário é bem-sucedido caso a variável *`vsaMetadata!.accountProviderIdentifier`* contém um valor válido e a data atual não passou o *`vsaMetadata!.authenticationExpirationDate`* valor.

</br>

#### Etapa &quot;Obter uma solicitação de perfil do Adobe para o MVPD selecionado&quot; {#Obtain_a_profile_request_from_Adobe_for_the_selected_MVPD}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio da Autenticação do Adobe Primetime [Solicitação de perfil](/help/authentication/retrieve-profilerequest.md) serviço.

>[!TIP]
>
> **<u>Dica Pro:</u>** Esteja ciente de que o identificador do provedor obtido da estrutura de conta do assinante de vídeo representa a variável *`platformMappingId`* em termos de configuração de autenticação do Adobe Primetime. Portanto, o aplicativo deve determinar o valor da propriedade de id do MVPD, usando o *`platformMappingId`* , por meio da Autenticação do Adobe Primetime [Fornecer Lista MVPD](/help/authentication/provide-mvpd-list.md) serviço.

</br>

#### Etapa: &quot;Encaminhe a solicitação do Adobe para o Platform SSO para obter o perfil&quot; {#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio do [Conta de assinante de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) estrutura.


- O aplicativo teria que verificar [permissão de acesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) as informações de assinatura do usuário e continue somente se o usuário tiver permitido.
- O pedido deverá apresentar um pedido [solicitação](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadatarequest) para informações de conta de assinante.
- O aplicativo teria que aguardar e processar a variável [metadados](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmetadata) informações.

 

>[!TIP]
>
> **<u>Dica Pro:</u>** Siga o trecho do código e preste atenção nos comentários.

```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                        // Construct the request for subscriber account information.
                        let vsaMetadataRequest: VSAccountMetadataRequest = VSAccountMetadataRequest();
    
                        // This is actually the SAML Issuer not the channel ID.
                        vsaMetadataRequest.channelIdentifier = "https://saml.sp.auth.adobe.com";
        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAccountProviderIdentifier = true;
                        
                        // This is going to include subscription account information which should match the provider determined in a previous step.
                        vsaMetadataRequest.includeAuthenticationExpirationDate = true;
                        
                        // This is going to make the Video Subscriber Account framework to refrain from prompting the user with the providers picker at this step. 
                        vsaMetadataRequest.isInterruptionAllowed = false;
    
                        // This are the user metadata fields expected to be available on a successful login and are determined from the [Adobe Primetime Authentication](/help/authentication/provide-mvpd-list.md) service. Look for the requiredMetadataFields associated with the provider determined in a previous step.
                        vsaMetadataRequest.attributeNames = requiredMetadataFields;
    
                        // This is the payload from [Adobe Primetime Authentication](/help/authentication/retrieve-profilerequest.md) service.
                        vsaMetadataRequest.verificationToken = profileRequestPayload;
                        
                        // Submit the request for subscriber account information.
                        videoSubscriberAccountManager.enqueue(vsaMetadataRequest) { vsaMetadata, vsaError in
                            if (vsaMetadata != nil && vsaMetadata!.samlAttributeQueryResponse != nil) {
                                var samlResponse: String? = vsaMetadata!.samlAttributeQueryResponse!;
                                
                                // Remove new lines, new tabs and spaces.
                                samlResponse = samlResponse?.replacingOccurrences(of: "[ \\t]+", with: " ", options: String.CompareOptions.regularExpression);
                                samlResponse = samlResponse?.components(separatedBy: CharacterSet.newlines).joined(separator: "");
                                samlResponse = samlResponse?.trimmingCharacters(in: CharacterSet.whitespacesAndNewlines);
                                
                                // Base64 encode.
                                samlResponse = samlResponse?.data(using: .utf8)?.base64EncodedString(options: []);
                                
                                // URL encode. Please be aware not to double URL encode it further.
                                samlResponse = samlResponse?.addingPercentEncoding(withAllowedCharacters: CharacterSet.init(charactersIn: "!*'();:@&=+$,/?%#[]").inverted);
                                
                                // Continue with the "Exchange the Platform SSO profile for an Adobe authentication token" step.
                                ...
                            } else {
                                // Fallback to regular authentication workflow.
                                ...
                            }
                        }
                        
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                    // Fallback to regular authentication workflow.
                    ...
                }
    }
    ...
```

</br>

#### Etapa: &quot;Troque o perfil de SSO da plataforma por um token de autenticação de Adobe&quot; {#Exchange_the_Platform_SSO_profile_for_an_Adobe_authentication_token}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio da Autenticação do Adobe Primetime [Troca de Token](/help/authentication/token-exchange.md) serviço.


>[!TIP]
>
> **<u>Dica Pro:</u>** Esteja ciente do trecho de código do [&quot;Encaminhe a solicitação do Adobe para o Platform SSO para obter o perfil&quot;](#Forward_the_Adobe_request_to_Platform_SSO_to_obtain_the_profile) etapa. Essa *`vsaMetadata!.samlAttributeQueryResponse!`* representa a variável *`SAMLResponse`*, que deve ser transmitida [Troca de Token](/help/authentication/token-exchange.md) e requer manipulação e codificação de sequência de caracteres (*Base64* codificado e *URL* codificado posteriormente) antes de fazer a chamada.

</br>

#### Etapa: &quot;O token de Adobe é gerado com êxito?&quot; {#Is_Adobe_token_generated_successfully}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio da autenticação da mídia Adobe Primetime [Troca de Token](/help/authentication/token-exchange.md) resposta bem-sucedida, que será uma *`204 No Content`*, indicando que o token foi criado com êxito e está pronto para ser usado para os fluxos de autorização.

</br>

#### Etapa: &quot;Iniciar fluxo de trabalho de autenticação de segunda tela&quot; {#Initiate_second_screen_authentication_workflow}

**Importante:** A terminologia &quot;workflow de autenticação de segunda tela&quot; é adequada para AppleTVs, enquanto a terminologia &quot;workflow de autenticação de primeira tela&quot; / &quot;Workflow de autenticação regular&quot; seria mais apropriada para iPhones e iPads.


>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio da Autenticação do Adobe Primetime

[Solicitação de código de registro](/help/authentication/registration-code-request.md), [Iniciar Autenticação](/help/authentication/initiate-authentication.md) e [Token de autenticação de recuperação de API REST](/help/authentication/retrieve-authentication-token.md) ou [Verificar Token de Autenticação](/help/authentication/check-authentication-token.md) serviços.


>[!TIP]
>
> **<u>Dica Pro:</u>** Siga as etapas abaixo para as implementações de tvOS.

- O pedido teria de [obter um código de registro](/help/authentication/registration-code-request.md) e apresentá-lo ao usuário final no primeiro dispositivo (tela).
- O pedido teria de ser iniciado [pesquisa para confirmar o estado de autenticação](/help/authentication/retrieve-authentication-token.md) no primeiro dispositivo (ecrã) após obtenção do código de registro.
- Outro pedido teria de ser [iniciar autenticação](/help/authentication/initiate-authentication.md) em um segundo dispositivo (tela) quando o código de registro é usado.
- O pedido teria de parar [sondagem](/help/authentication/retrieve-authentication-token.md) no primeiro dispositivo (tela) quando o token de autenticação é gerado.

 

>[!TIP]
>
> **<u>Dica Pro:</u>** Siga as etapas abaixo para as implementações do iOS/iPadOS.

- O pedido teria de [obter um código de registro](/help/authentication/registration-code-request.md) que não deve ser apresentado ao usuário final no primeiro dispositivo (tela).
- O pedido teria de [iniciar autenticação](/help/authentication/initiate-authentication.md) no primeiro dispositivo (ecrã) utilizando o código de registro e um [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) ou [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) componente.
- O pedido teria de ser iniciado [sondagem para conhecer o estado de autenticação](/help/authentication/retrieve-authentication-token.md) no primeiro dispositivo (tela) após a [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) ou [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) fecha o componente.
- O pedido teria de parar [sondagem](/help/authentication/retrieve-authentication-token.md) no primeiro dispositivo (tela) quando o token de autenticação é gerado.

</br>

#### Etapa: &quot;Prosseguir com os fluxos de autorização&quot; {#Proceed_with_authorization_flows}

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio da Autenticação do Adobe Primetime [Iniciar Autorização](/help/authentication/initiate-authorization.md) e [Obter token de mídia curta](/help/authentication/obtain-short-media-token.md) serviços.

</br>

### Logout {#Logout}

O [Conta de assinante de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) O framework não fornece uma API para fazer logoff programaticamente de pessoas que entraram em sua conta do provedor de TV no nível do sistema do dispositivo. Portanto, para que o logout tenha efeito total, o usuário final teria que fazer logoff explicitamente de *`Settings -> TV Provider`* no iOS/iPadOS ou *`Settings -> Accounts -> TV Provider`* no tvOS. A outra opção que o usuário teria é retirar a permissão para acessar as informações de assinatura do usuário na seção de configurações específicas do aplicativo (acesso do Provedor de TV).

>[!TIP]
>
> **<u>Dica:</u>** Implemente isso por meio da Autenticação do Adobe Primetime [Chamada de metadados do usuário](/help/authentication/user-metadata.md) e [Logout](/help/authentication/initiate-logout.md) serviços.


>[!TIP]
>
> **<u>Dica Pro:</u>** Siga as etapas abaixo para as implementações de tvOS.
 

- O aplicativo teria que determinar se a autenticação ocorreu como resultado de um logon por meio do SSO da plataforma ou não, usando o &quot;*tokenSource&quot;* [metadados do usuário](/help/authentication/user-metadata.md) do serviço Adobe Primetime Authentication.
- O aplicativo teria que instruir/solicitar que o usuário saia explicitamente do *`Settings -> Accounts -> TV Provider`* no tvOS **only** no caso de *&quot;tokenSource&quot;* é igual a &quot;*Apple&quot;.*
- O pedido teria de [iniciar o logout](/help/authentication/initiate-logout.md) do serviço Adobe Primetime Authentication usando uma chamada HTTP direta. Isso não facilitaria a limpeza da sessão no lado do MVPD.

 

>[!TIP]
>
> **<u>Dica Pro:</u>** Siga as etapas abaixo para as implementações do iOS/iPadOS.

- O aplicativo teria que determinar se a autenticação ocorreu como resultado de um logon por meio do SSO da plataforma ou não, usando o &quot;*tokenSource&quot;* [metadados do usuário](/help/authentication/user-metadata.md) do serviço Adobe Primetime Authentication.
- O aplicativo teria que instruir/solicitar que o usuário saia explicitamente do *`Settings -> TV Provider`* no iOS/iPadOS **only** no caso de *&quot;tokenSource&quot;* é igual a *&quot;Apple&quot;*.
- O pedido teria de [iniciar o logout](/help/authentication/initiate-logout.md) do serviço Adobe Primetime Authentication usando um [WKWebView](https://developer.apple.com/documentation/webkit/wkwebview) ou [SFSafariViewController](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller) componente. Isso facilitaria a limpeza da sessão no lado do MVPD.

<!--

## Resources

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [REST API Overview](/help/authentication/rest-api-overview.md)
- [REST API Cookbook (Server-to-Server)](/help/authentication/rest-api-cookbook-servertoserver.md)
- [REST API Cookbook (Client-to-Server)](/help/authentication/rest-api-cookbook-clienttoserver.md)
- [REST API Reference](/help/authentication/rest-api-reference.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->

