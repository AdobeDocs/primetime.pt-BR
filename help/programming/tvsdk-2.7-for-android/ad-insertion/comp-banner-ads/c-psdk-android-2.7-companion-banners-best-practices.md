---
title: Práticas recomendadas para anúncios de banner complementares
description: Práticas recomendadas para anúncios de banner complementares
copied-description: true
exl-id: 9a335dfc-3de2-45bf-b17e-0330a5d50606
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Anúncios de banner de companhia {#companion-banner-ads}

O TVSDK é compatível com anúncios de banner complementares, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o fim do anúncio linear. Seu aplicativo é responsável por exibir os banners de companhia que são fornecidos com um anúncio linear.

## Práticas recomendadas para anúncios de banner complementares {#best-practices-for-companion-banner-ads}

Ao exibir anúncios complementares, siga estas recomendações:

* Tente apresentar quantos anúncios de banner complementares de um anúncio de vídeo couberem no layout do reprodutor.
* Apresente um banner complementar somente se você tiver um local que corresponda à altura e à largura especificadas do anúncio.

   >[!IMPORTANT]
   >
   >Não redimensione o anúncio.

* Comece a apresentar os banner(s) complementar(es) o mais rápido possível após o início do anúncio.
* Não sobreponha o container principal de anúncios/vídeos com banners complementares.
* Você pode exibir banners companheiros após o fim do anúncio.

   A prática padrão é exibir cada banner complementar até que você tenha uma substituição para o anúncio.
