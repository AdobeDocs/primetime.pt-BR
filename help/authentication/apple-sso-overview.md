---
title: Visão geral do Apple SSO
description: Visão geral do Apple SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---



# Visão geral do Apple SSO {#apple-sso-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Introdução {#Introduction}

O Apple fornece uma API que permite que as pessoas façam logon em sua conta de provedor de TV no nível do sistema do dispositivo, eliminando a necessidade de autenticação por aplicativo.

Assim, a Apple e a Adobe Primetime Authentication se uniram para criar a experiência de usuário da plataforma Single Sign-On (SSO) no ecossistema da TV em qualquer lugar para os proprietários de iPhone, iPad e Apple TV.

Para se beneficiar da experiência do usuário de Logon único (SSO) em um dispositivo Apple, há uma lista de pré-requisitos que devem ser concluídos.

</br>

## Pré-requisitos {#Prerequisites}

O pré-requisito pode se aplicar a uma ou várias entidades envolvidas no negócio TVE, como Programadores, MVPDs, Autenticação Adobe Primetime ou Apple.

</br>

### Programador {#Programmer}

Para se beneficiar da experiência do usuário de Logon único (SSO), um Programador deve:

1. Use pelo menos o Xcode versão 8 e o iOS/tvOS versão 10.

1. Tenha a [Direito de logon único do assinante de vídeo](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) configurado para sua conta de desenvolvedor do Apple. Entre em contato com a Apple para ativar [Estrutura da conta do assinante de vídeo](https://developer.apple.com/documentation/videosubscriberaccount) para sua ID da equipe da Apple.

1. Habilite o Logon Único (YES) para cada integração desejada (Canal x MVPD) e a plataforma desejada (iOS / tvOS) por meio da [Painel Adobe Primetime TVE](https://console.auth.adobe.com/).

1. Integre os workflows SSO do Apple usando uma das duas soluções a seguir oferecidas pela equipe de Autenticação da Adobe Primetime:

   - A API REST de autenticação da Adobe Primetime pode ser compatível com a autenticação de logon único (SSO) da plataforma para usuários finais de aplicativos clientes em execução no iOS, iPadOS ou tvOS. Consulte também [Guia SSO do Apple (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md).

   - O SDK iOS/tvOS do Adobe Primetime Authentication AccessEnabler pode oferecer suporte à autenticação de logon único (SSO) da plataforma para usuários finais de aplicativos clientes em execução no iOS, iPadOS ou tvOS. Consulte também [Guia SSO do Apple (SDK do iOS/tvOS)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

   - **<u>Dica Pro:</u>** Para ter acesso às informações de assinatura do usuário, o usuário deve conceder ao aplicativo permissão para continuar, de modo semelhante ao acesso à câmera ou ao microfone do dispositivo. Essa permissão deve ser solicitada por aplicativo e o dispositivo salvará a seleção do usuário. Lembre-se de que o usuário pode alterar sua decisão acessando as configurações do aplicativo (acesso de permissão do provedor de TV) ou a seção de *`Settings -> TV Provider`* no iOS/iPadOS ou *`Settings -> Accounts -> TV Provider`* no tvOS.

   - **<u>Dica Pro:</u>** Recomendamos solicitar a permissão do usuário quando o aplicativo entrar no estado de primeiro plano, mas é apenas uma sugestão, pois o aplicativo pode verificar [permissão de acesso](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) as informações de assinatura do usuário em qualquer ponto antes de exigir autenticação do usuário. Além disso, as APIs do SDK do AccessEnabler iOS/tvOS solicitarão automaticamente a permissão do usuário quando necessário.

   - **<u>Dica Pro:</u>** Recomendamos incentivar os usuários que se recusam a conceder permissão de acesso às informações de assinatura explicando os benefícios da experiência do usuário de Logon único (SSO). Lembre-se de que o usuário pode alterar sua decisão acessando as configurações do aplicativo (acesso de permissão do provedor de TV) ou a seção de *`Settings -> TV Provider`* no iOS/iPadOS ou *`Settings -> Accounts -> TV Provider`* no tvOS.

O resultado deve criar uma experiência de acordo com os seguintes fluxos de usuário, o que sugerimos que você consulte antes de começar a desenvolver seus aplicativos:

- [iPhone / iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) fluxos de usuário
- [Apple TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) fluxos de usuário


>[!IMPORTANT]
>
> Quando o recurso de logon único é **ativado** para iOS/tvOS **e** no caso da Apple **integrado (compatível) ou selecionador** MVPDs os fluxos de autenticação/logout dos workflows do Apple SSO envolverão as soluções de Autenticação da Apple e da Adobe Primetime, enquanto todos os outros fluxos (autorização, pré-autorização, metadados, etc.) serão atendidos exclusivamente pela Autenticação Adobe Primetime.


>[!IMPORTANT]
>
> Quando o recurso de logon único é **desativado** para iOS/tvOS **ou** no caso da Apple **não integrado (não suportado)** MVPDs os fluxos de autenticação/logout serão fallback dos workflows SSO do Apple para os regulares servidos apenas pela Autenticação Adobe Primetime.


>[!IMPORTANT]
>
> Um ganho principal do fluxo de trabalho SSO do Apple é representado pelo fluxo de usuário de autenticação de tela única, que também pode ser entregue em TVs Apple quando o recurso Logon único é **ativado** para tvOS **e** no caso da Apple **integrado (compatível)** MVPDs.


### MVPD {#MVPD}

Para se beneficiar da experiência do usuário de Logon Único (SSO), um MVPD deve:

 

1. Ser integrado ao workflow SSO do Apple no lado do Apple. Entre em contato com a Apple para facilitar o processo de integração.
1. Forneça um aplicativo TVML JavaScript capaz de manipular o formulário de logon do usuário. Entre em contato com a Apple para receber a documentação adequada.
1. Forneça um valor de string representando o identificador do provedor atribuído pela Apple durante o processo de integração. Entre em contato com a Autenticação do Adobe Primetime para executar as alterações de configuração.

</br>

## Perguntas frequentes {#FAQ}

1. Caso algo dê errado com o fluxo de trabalho do Apple SSO, o aplicativo que usa o SDK do AccessEnabler iOS/tvOS pode fallback para o fluxo de autenticação regular?
   - Isso é possível, mas requer que uma alteração de configuração seja executada no [Painel Adobe Primetime TVE](https://console.auth.adobe.com/). O *Habilitar logon único* deve ser definido em *NÃO* para a integração desejada (Canal x MVPD) e a plataforma desejada (iOS/tvOS).
   - O aplicativo só reconheceria a alteração de configuração depois de chamar [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) Caso esteja usando o SDK do AccessEnabler iOS/tvOS.
1. O aplicativo saberá quando uma autenticação aconteceu como resultado de um logon por meio do SSO da plataforma em outro dispositivo ou outro aplicativo?
   - Essas informações não estarão disponíveis.
1. O aplicativo saberá quando uma autenticação aconteceu como resultado de um logon por meio do SSO da plataforma no mesmo dispositivo? 
   - Essas informações estão disponíveis como parte da chave de metadados do usuário: *tokenSource*, que deve retornar o valor da string: &quot;Apple&quot; neste caso.
1. O que acontece se um usuário faz logon acessando o *`Settings -> TV Provider`* no iOS/iPadOS ou *`Settings -> Accounts -> TV Provider`* na seção tvOS usando um MVPD que não está integrado ao aplicativo?
   - Quando o usuário inicia o aplicativo, ele não é autenticado por meio do workflow Apple SSO. Portanto, o aplicativo teria que fallback para o fluxo de autenticação regular e apresentar seu próprio seletor de MVPD.
1. O que acontece se um usuário faz logon acessando o *`Settings -> TV Provider`* no iOS/iPadOS ou *`Settings -> Accounts -> TV Provider`* na seção tvOS usando um MVPD que tem o *Habilitar logon único* definir em *NÃO* no [Painel Adobe Primetime TVE](https://console.auth.adobe.com/) para plataforma iOS/tvOS?
   - Quando o usuário inicia o aplicativo, ele não é autenticado por meio do workflow Apple SSO. Portanto, o aplicativo teria que fallback para o fluxo de autenticação regular e apresentar seu próprio seletor de MVPD.
1. O que acontece se um usuário tem um MVPD que não é integrado (não é suportado) pelo Apple, mas que está presente no seletor do Apple?
   - Quando o usuário inicia o aplicativo, ele só seleciona o MVPD por meio do workflow SSO do Apple sem concluir o fluxo de autenticação. Portanto, o aplicativo teria que fallback para o fluxo de autenticação regular, mas poderia usar o MVPD já selecionado.
1. O que acontece se um usuário tem um MVPD que não é integrado (não é suportado) pelo Apple?
   - Quando o usuário iniciar o aplicativo, ele selecionará a opção de seletor &quot;Outros provedores de TV&quot; por meio do fluxo de trabalho do Apple SSO. Portanto, o aplicativo teria que fallback para o fluxo de autenticação regular e apresentar seu próprio seletor de MVPD.
1. O que acontece se um usuário tem um MVPD que é degradado através de [Painel Adobe Primetime TVE](https://console.auth.adobe.com/)?
   - Quando o usuário inicia o aplicativo, ele é autenticado por meio do mecanismo de degradação e não por meio do workflow Apple SSO.
   - A experiência deve ser contínua para o usuário, enquanto o aplicativo será informado por meio do *N010* código de aviso caso esteja usando o SDK do AccessEnabler iOS/tvOS.
1. A ID de usuário do MVPD será alterada entre o Apple SSO e o fluxo de autenticação SSO não-Apple?
   - A expectativa é que a ID do usuário não mude, mas precise ser verificada para cada provedor selecionado. 
1. Haverá alguma alteração nos TTLs de autenticação?
   - A Autenticação Adobe Primetime continuará a respeitar os TTLs exigidos pelos Programadores para sua integração com cada MVPD.
   - Ao navegar de um aplicativo do Programador para outro aplicativo do Programador por meio do SSO do Apple, o segundo aplicativo terá o TTL de sua integração do Programador x MVPD correspondente (ele não compartilhará o TTL do primeiro aplicativo que se autentica)

|  | TTL de autenticação do Adobe Primetime expirado | TTL de autenticação do Adobe Primetime válido |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **TTL do token de dispositivo Apple expirado** | O usuário NÃO é autenticado (o seletor MVPD deve aparecer) | O usuário é autenticado e o TTL é o tempo restante de seu token de autenticação do Adobe Primetime |
| **TTL do token de dispositivo Apple válido** | O usuário é autenticado silenciosamente e obtém outro token de autenticação do Adobe Primetime com o TTL especificado no Painel TVE | O usuário é autenticado e o TTL é o tempo restante de seu token de autenticação do Adobe Primetime |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
