---
description: nulo
seo-description: nulo
seo-title: Práticas recomendadas para anúncios em banners companheiros
title: Práticas recomendadas para anúncios em banners companheiros
uuid: 0e4c98cd-5e16-4c84-848f-02bc6f1b0d6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Práticas recomendadas para anúncios em banners companheiros {#best-practices-for-companion-banner-ads}

O TVSDK oferece suporte a anúncios de banners companheiros, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o término do anúncio linear. Seu aplicativo é responsável por exibir os banners associados que são fornecidos com um anúncio linear.

Ao exibir anúncios complementares, siga estas recomendações:

* Tente apresentar tantos anúncios de banner companion de um anúncio de vídeo quantos couberem no layout do player.
* Apresente um banner complementar somente se você tiver um local que corresponda à altura e largura especificadas do anúncio.

   >[!IMPORTANT]
   >
   >Não redimensione o anúncio.

* Comece a apresentar os banners companheiros assim que possível após o início do anúncio.
* Não sobreponha o container principal de anúncio/vídeo com banners companheiros.
* Você pode exibir banners complementares após o término do anúncio.

A prática padrão é exibir cada banner complementar até que você tenha uma substituição para o anúncio.