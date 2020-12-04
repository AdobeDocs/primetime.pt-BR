---
description: Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK escute eventos relacionados a anúncios.
seo-description: Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK escute eventos relacionados a anúncios.
seo-title: Exibir anúncios em banners
title: Exibir anúncios em banners
uuid: cfd4b26c-9643-4b60-9aff-bc27dec289f1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Exibir anúncios em banners {#display-banner-ads}

Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK escute eventos relacionados a anúncios.

O TVSDK fornece uma lista de anúncios de banner associados a um anúncio linear por meio do evento `AdPlaybackEventListener.onAdBreakStart`.

Os manifestos podem especificar anúncios de banner companheiro:

* Um trecho HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou um arquivo SWF de Flash Adobe

Para cada anúncio complementar, o TVSDK indica quais tipos estão disponíveis para seu aplicativo.

1. Adicione um ouvinte para o evento `AdPlaybackEventListener.onAdBreakStart` que faça o seguinte:

   * Limpa os anúncios existentes na instância do banner.
   * Obtém a lista de anúncios complementares de `Ad.getCompanionAssets`.
   * Se a lista de anúncios complementares não estiver vazia, repita a lista para ver as instâncias de banner.

      Cada instância do banner (um `AdAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
   * Se um anúncio de vídeo não tiver anúncios adicionais reservados, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.
   * Para mostrar um anúncio de exibição independente, adicione a lógica ao script para executar uma tag de anúncio de exibição DFP normal (DoubleClick for Publishers) na instância apropriada do banner.
   * Envia as informações do banner para uma função na sua página que exibe os banners em um local apropriado.

      Geralmente é um `div`, e sua função usa `div ID` para exibir o banner.