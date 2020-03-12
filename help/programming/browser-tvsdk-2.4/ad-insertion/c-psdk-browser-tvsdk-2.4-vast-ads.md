---
description: Quando o TVSDK do navegador solicita um anúncio que não está em seu servidor de publicidade primário, o player precisa solicitar o anúncio do servidor secundário. O VAST (Video Ad Serving Template) define o padrão de comunicação entre servidores de anúncios e players de vídeo e é a resposta enviada pelo servidor de anúncios secundário quando o anúncio é solicitado.
seo-description: Quando o TVSDK do navegador solicita um anúncio que não está em seu servidor de publicidade primário, o player precisa solicitar o anúncio do servidor secundário. O VAST (Video Ad Serving Template) define o padrão de comunicação entre servidores de anúncios e players de vídeo e é a resposta enviada pelo servidor de anúncios secundário quando o anúncio é solicitado.
seo-title: Anúncios VAST
title: Anúncios VAST
uuid: 052dae0c-2425-456c-aebe-531f68bb5aa8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Anúncios VAST {#vast-ads}

Quando o TVSDK do navegador solicita um anúncio que não está em seu servidor de publicidade primário, o player precisa solicitar o anúncio do servidor secundário. O VAST (Video Ad Serving Template) define o padrão de comunicação entre servidores de anúncios e players de vídeo e é a resposta enviada pelo servidor de anúncios secundário quando o anúncio é solicitado.

Para obter mais informações sobre o VAST, consulte Modelo de serviço de anúncio de vídeo [digital (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

O TVSDK do navegador suporta os seguintes elementos de anúncio VAST:

## Anúncios embutidos e em linha {#section_11B8A1A8F52F4F77981C6AAC02185087}

Os seguintes elementos são suportados:

* **`wrapper`** Quando o player precisar entrar em contato com um servidor de anúncios secundário para solicitar um anúncio, o elemento wrapper fornecerá as informações de redirecionamento. Um elemento de invólucro pode apontar para vários invólucros que, em última análise, apontam para um anúncio VAST.

* **`inline`** Os seguintes elementos obrigatórios são suportados:

* `AdSystem`
* `AdTitle`
* `Impression`

   Os seguintes elementos opcionais são suportados:

* `Description`
* `Survey`
* `Error`

## Creative {#section_0121F948CB074E49A8132D202786CAA4}

Este elemento é um arquivo que faz parte de um anúncio VAST e contém um `creative` elemento que pode suportar um anúncio linear, um anúncio não linear ou um anúncio complementar. No `creative` elemento, os elementos `id`, `sequence`e `adId` são suportados.

Estas são mais informações sobre os tipos de anúncios:

* **Anúncios** lineares Os seguintes elementos são suportados:

   * `TrackingEvent`, que contém o `Tracking` elemento .
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, incluindo:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`
         [!TIP]
Nesse elemento, os atributos `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework`e `type` são suportados.

* **Anúncios** não lineares Os seguintes elementos são suportados:

   * `Non-linear`
      [!TIP]
Nesse elemento, os atributos `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio`e `minSuggestedDuration` são suportados.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Anúncios** complementares Os seguintes elementos são suportados:

   * `Companion`
      [!TIP]
Neste elemento, os atributos `id`, `width`, `height`, `apiFramework`, `expandedWidth`e `expandedHeight` são suportados.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Extensões {#section_17401C75F419453BAE83637EEB6E1E60}

[!TIP]
Somente as extensões específicas do Auditude são suportadas.

* `Extension`