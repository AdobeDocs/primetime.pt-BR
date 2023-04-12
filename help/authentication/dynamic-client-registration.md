---
title: Registro dinâmico de clientes
description: Registro dinâmico de clientes
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Registro dinâmico de clientes {#dynamic-client-registration}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Contexto {#context}

Para se alinhar às práticas modernas de segurança, aos requisitos aprimorados de UX e proprietários da plataforma, o SDK do Android de Autenticação da Adobe Primetime e o SDK do iOS estão avançando na direção da adoção [Guias personalizadas do Android Chrome](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari view controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}.

A implementação atual do AdobePass usa exibições da Web específicas da plataforma, para fornecer o ambiente da Web para exibir a página de logon do MVPD. Essas exibições da Web não compartilham o gerenciamento de credenciais com navegadores da plataforma, portanto, o usuário não pode usar uma senha salva pelo navegador ao usar um aplicativo de Autenticação do Adobe Primetime. Além disso, por motivos de segurança, algumas plataformas estão se movendo para descontinuar os controladores WebView para tarefas de autenticação. O Google e o Apple fornecem opções alternativas, como &quot;Guias personalizadas do Chrome&quot; e &quot;Controlador de exibição do Safari&quot;. São basicamente guias de uso único de seus respectivos navegadores. A Autenticação Adobe Primetime adotará esses novos componentes em 2018.

## Detalhes {#details}

Atualmente, há duas maneiras pelas quais a Autenticação Adobe Pass identifica e registra aplicativos:

* clientes baseados em navegador são registrados por meio da listagem de domínio permitida
* clientes de aplicativos nativos, como aplicativos iOS e Android, são registrados por meio do mecanismo de solicitação assinado

Para abordar os novos fluxos para o Chrome Custom Tabs &amp; Safari View Controller, a Adobe Pass propõe um novo mecanismo de registro de cliente para registrar novos aplicativos. Esse mecanismo permitirá um controle mais seguro e granular de seus aplicativos e poderá ser usado para registrar aplicativos em todas as plataformas.

<!--
## Related Information

- [Dynamic Client Registration API](/help/authentication/dynamic-client-registration-api.md)
- [Dynamic Client Registration Management](/help/authentication/dynamic-client-registration-management.md)
-->