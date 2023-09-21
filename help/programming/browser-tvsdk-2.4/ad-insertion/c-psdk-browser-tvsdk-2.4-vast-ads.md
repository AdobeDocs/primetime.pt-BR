---
description: Quando o TVSDK do navegador solicita um anúncio que não está no servidor de anúncios principal, o reprodutor precisa solicitar o anúncio do servidor secundário. O Modelo de veiculação de anúncios de vídeo (VAST) define o padrão de comunicação entre servidores de publicidade e players de vídeo e é a resposta enviada pelo servidor de publicidade secundário quando o anúncio é solicitado.
title: Anúncios VAST
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Anúncios VAST {#vast-ads}

Quando o TVSDK do navegador solicita um anúncio que não está no servidor de anúncios principal, o reprodutor precisa solicitar o anúncio do servidor secundário. O Modelo de veiculação de anúncios de vídeo (VAST) define o padrão de comunicação entre servidores de publicidade e players de vídeo e é a resposta enviada pelo servidor de publicidade secundário quando o anúncio é solicitado.

Para obter mais informações sobre o VAST, consulte [Modelo de veiculação de anúncio de vídeo digital (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

O TVSDK do navegador é compatível com os seguintes elementos de anúncio VAST:

## Anúncios em linha e em invólucro {#section_11B8A1A8F52F4F77981C6AAC02185087}

Os seguintes elementos são compatíveis:

* **`wrapper`** Quando o reprodutor precisa entrar em contato com um servidor de anúncios secundário para solicitar um anúncio, o elemento invólucro fornece as informações de redirecionamento. Um elemento de invólucro pode apontar para vários invólucros que apontam para um anúncio VAST.

* **`inline`** Os seguintes elementos obrigatórios são compatíveis:

* `AdSystem`
* `AdTitle`
* `Impression`

  Os seguintes elementos opcionais são compatíveis:

* `Description`
* `Survey`
* `Error`

## Criativos {#section_0121F948CB074E49A8132D202786CAA4}

Este elemento é um arquivo que faz parte de um anúncio VAST e contém um `creative` elemento que pode suportar um anúncio linear, um anúncio não linear ou um anúncio complementar. No `creative` elemento, a variável `id`, `sequence`, e `adId` Os elementos do são compatíveis.

Veja a seguir mais informações sobre os tipos de anúncios:

* **Anúncios lineares** Os seguintes elementos são compatíveis:

   * `TrackingEvent`, que contém a `Tracking` elemento.
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
        >Neste elemento, a variável `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework`, e `type` atributos são compatíveis.

* **Anúncios não lineares** Os seguintes elementos são compatíveis:

   * `Non-linear`

     >[!TIP]
     >
     >Neste elemento, a variável `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio`, e `minSuggestedDuration` atributos são compatíveis.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Anúncios de companhia** Os seguintes elementos são compatíveis:

   * `Companion`

     >[!TIP]
     >
     >Neste elemento, a variável `id`, `width`, `height`, `apiFramework`, `expandedWidth`, e `expandedHeight` atributos são compatíveis.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Extensões {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Somente as extensões específicas do Auditude são suportadas.

* `Extension`
