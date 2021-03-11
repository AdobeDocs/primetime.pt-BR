---
title: Práticas recomendadas para anúncios em banners complementares
description: Práticas recomendadas para anúncios em banners complementares
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Anúncios de banner complementares {#companion-banner-ads}

O TVSDK suporta anúncios de banner complementar, que são anúncios que acompanham um anúncio linear e que geralmente permanecem na página depois que o anúncio linear termina. Seu aplicativo é responsável por exibir os banners complementares que são fornecidos com um anúncio linear.

## Práticas recomendadas para anúncios de banner complementar {#best-practices-for-companion-banner-ads}

Ao exibir anúncios complementares, siga estas recomendações:

* Tente apresentar o máximo possível de anúncios de banner complementares de um anúncio de vídeo que couberem no layout do player.
* Apresente um banner complementar somente se você tiver um local que corresponda à altura e largura especificadas para o anúncio.

   >[!IMPORTANT]
   >
   >Não redimensione o anúncio.

* Comece a apresentar o(s) banner(s) complementar(es) assim que possível após o início do anúncio.
* Não sobreponha o contêiner principal de anúncio/vídeo com banners complementares.
* Você pode exibir banners complementares depois que o anúncio terminar.

   A prática padrão é exibir cada banner complementar até que você tenha um substituto para o anúncio.

