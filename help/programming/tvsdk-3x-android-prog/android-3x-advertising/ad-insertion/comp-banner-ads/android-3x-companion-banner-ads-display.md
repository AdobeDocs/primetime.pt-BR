---
description: Para exibir anúncios de banner, você precisa criar instâncias de banner e permitir que o TVSDK acompanhe eventos relacionados a anúncios.
title: Exibir anúncios de banner
exl-id: 3ccf6525-ffc1-4f45-a662-8b53cab0f448
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Exibir anúncios de banner {#display-banner-ads}

Para exibir anúncios de banner, você precisa criar instâncias de banner e permitir que o TVSDK acompanhe eventos relacionados a anúncios.

O TVSDK fornece uma lista de anúncios de banner complementares associados a um anúncio linear por meio do `AdPlaybackEventListener.onAdBreakStart` evento.

Os manifestos podem especificar anúncios de banner complementares por:

* Um trecho de HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou de um arquivo SWF de Adobe Flash

Para cada anúncio complementar, o TVSDK indica quais tipos estão disponíveis para seu aplicativo.

1. Adicione um ouvinte para o `AdPlaybackEventListener.onAdBreakStart` evento que faz o seguinte:

   * Limpa os anúncios existentes na instância do banner.
   * Obtém a lista de anúncios complementares de `Ad.getCompanionAssets`.
   * Se a lista de anúncios complementares não estiver vazia, repita sobre a lista para instâncias de banner.

      Cada instância do banner (uma `AdAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
   * Se um anúncio de vídeo não tiver anúncios complementares reservados com ele, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.
   * Para mostrar um anúncio de exibição independente, adicione a lógica ao script para executar uma tag de anúncio de exibição DFP (DoubleClick for Publishers) normal na instância de banner apropriada.
   * Envia as informações do banner para uma função na página que exibe os banners no local apropriado.

      Isso geralmente é um `div`, e sua função usa o `div ID` para exibir o banner.
