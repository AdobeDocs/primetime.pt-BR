---
description: Quando o TVSDK do navegador solicita um anúncio que não esteja no servidor de anúncios principal, o reprodutor precisa solicitar o anúncio do servidor secundário. O VAST (Video Ad Serving Template) define o padrão de comunicação entre servidores de anúncios e reprodutores de vídeo e é a resposta enviada pelo servidor de anúncio secundário quando o anúncio é solicitado.
title: Anúncios VAST
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Anúncios VAST {#vast-ads}

Quando o TVSDK do navegador solicita um anúncio que não esteja no servidor de anúncios principal, o reprodutor precisa solicitar o anúncio do servidor secundário. O VAST (Video Ad Serving Template) define o padrão de comunicação entre servidores de anúncios e reprodutores de vídeo e é a resposta enviada pelo servidor de anúncio secundário quando o anúncio é solicitado.

Para obter mais informações sobre VAST, consulte [Modelo de veiculação de anúncio de vídeo digital (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

O TVSDK do navegador é compatível com os seguintes elementos de anúncio VAST:

## Anúncios em linha e do invólucro {#section_11B8A1A8F52F4F77981C6AAC02185087}

Os seguintes elementos são compatíveis:

* **`wrapper`** Quando o reprodutor precisa entrar em contato com um servidor de publicidade secundário para solicitar um anúncio, o elemento wrapper fornece as informações de redirecionamento. Um elemento wrapper pode apontar para vários wrappers que apontam para um anúncio VAST.

* **`inline`** Os seguintes elementos obrigatórios são suportados:

* `AdSystem`
* `AdTitle`
* `Impression`

   Os seguintes elementos opcionais são compatíveis:

* `Description`
* `Survey`
* `Error`

## Criações {#section_0121F948CB074E49A8132D202786CAA4}

Esse elemento é um arquivo que faz parte de um anúncio VAST e contém um elemento `creative` que pode suportar um anúncio linear, um anúncio não linear ou um anúncio complementar. No elemento `creative`, os elementos `id`, `sequence` e `adId` são compatíveis.

Estas são mais informações sobre os tipos de anúncios:

* **** Anúncios linearesOs seguintes elementos são compatíveis:

   * `TrackingEvent`, que contém o  `Tracking` elemento .
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, incluindo o seguinte:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

         >[!TIP]
         >
         >Neste elemento, os atributos `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework` e `type` são suportados.

* **** Anúncios não linearesOs seguintes elementos são compatíveis:

   * `Non-linear`

      >[!TIP]
      >
      >Neste elemento, os atributos `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio` e `minSuggestedDuration` são suportados.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **** Anúncios complementaresOs seguintes elementos são compatíveis:

   * `Companion`

      >[!TIP]
      >
      >Neste elemento, os atributos `id`, `width`, `height`, `apiFramework`, `expandedWidth` e `expandedHeight` são suportados.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Extensões {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Somente as extensões específicas do Auditude são suportadas.

* `Extension`
