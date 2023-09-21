---
title: Registro de cliente dinâmico
description: Registro de cliente dinâmico
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Registro de cliente dinâmico {#dynamic-client-registration}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Contexto {#context}

Para alinhar-se às práticas modernas de segurança, aos requisitos aprimorados de UX e proprietários de plataforma, o SDK Android da Autenticação da Adobe Primetime e o SDK da iOS estão evoluindo na direção da adoção [Guias personalizadas do Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

A implementação atual do AdobePass usa exibições da Web específicas da plataforma para fornecer o ambiente da Web para exibir a página de logon do MVPD. Essas exibições da Web não compartilham o gerenciamento de credenciais com navegadores de plataforma, portanto, o usuário não pode usar uma senha salva do navegador ao usar um aplicativo de Autenticação do Adobe Primetime. Além disso, por motivos de segurança, algumas plataformas estão mudando para descontinuar os controladores WebView para tarefas de autenticação. O Google e o Apple fornecem opções alternativas, como &quot;Guias personalizadas do Chrome&quot; e &quot;Controlador de exibição do Safari&quot;. Elas são basicamente guias de uso único dos respectivos navegadores. A autenticação da Adobe Primetime adotará esses novos componentes em 2018.

## Detalhes {#details}

Atualmente, há duas maneiras pelas quais a Autenticação Adobe Pass identifica e registra aplicativos:

* os clientes baseados em navegador são registrados por meio da lista de domínios permitidos
* os clientes de aplicativos nativos, como aplicativos iOS e Android, são registrados por meio do mecanismo solicitante assinado

Para lidar com os novos fluxos do Chrome Custom Guias e do Safari View Controller, a Adobe Pass propõe um novo mecanismo de registro do cliente para registrar novos aplicativos. Esse mecanismo permitirá um controle mais seguro e granular de seus aplicativos e poderá ser usado para registrar aplicativos em todas as plataformas.

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->
