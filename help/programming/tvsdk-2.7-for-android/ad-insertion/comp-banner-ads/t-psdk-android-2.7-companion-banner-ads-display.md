---
description: Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK escute eventos relacionados a anúncios.
seo-description: Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK escute eventos relacionados a anúncios.
seo-title: Exibir anúncios em banners
title: Exibir anúncios em banners
uuid: 7246dfab-860f-4b55-9554-49738a483406
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Exibir anúncios em banners {#display-banner-ads}

Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK escute eventos relacionados a anúncios.

O TVSDK fornece uma lista de anúncios de banner associados a um anúncio linear por meio do `AdPlaybackEventListener.onAdBreakStart` evento.

Os manifestos podem especificar anúncios de banner companheiro:

* Um trecho HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou de um arquivo Adobe Flash SWF

Para cada anúncio complementar, o TVSDK indica quais tipos estão disponíveis para seu aplicativo.

1. Adicione um ouvinte para o `AdPlaybackEventListener.onAdBreakStart` evento que faça o seguinte:

   * Limpa os anúncios existentes na instância do banner.
   * Obtém a lista de anúncios complementares de `Ad.getCompanionAssets`.
   * Se a lista de anúncios complementares não estiver vazia, passe o mouse sobre a lista para ver as instâncias de banner.

      Cada instância do banner (an `AdAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
   * Se um anúncio de vídeo não tiver anúncios complementares reservados, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.
   * Para mostrar um anúncio de exibição independente, adicione a lógica ao script para executar uma tag de anúncio de exibição DFP normal (DoubleClick for Publishers) na instância apropriada do banner.
   * Envia as informações do banner para uma função na sua página que exibe os banners em um local apropriado.

      Geralmente, isso é uma `div`função e sua função usa o `div ID` para exibir o banner.

