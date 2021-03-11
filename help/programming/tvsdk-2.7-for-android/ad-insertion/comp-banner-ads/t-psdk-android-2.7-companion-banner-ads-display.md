---
description: Para exibir anúncios de banner, é necessário criar instâncias de banner e permitir que o TVSDK acompanhe eventos relacionados a anúncios.
title: Exibir anúncios de banner
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Exibir anúncios de banner {#display-banner-ads}

Para exibir anúncios de banner, é necessário criar instâncias de banner e permitir que o TVSDK acompanhe eventos relacionados a anúncios.

O TVSDK fornece uma lista de anúncios de banner complementar associados a um anúncio linear por meio do evento `AdPlaybackEventListener.onAdBreakStart`.

Os manifestos podem especificar anúncios de banner complementar ao:

* Um trecho HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou um arquivo SWF de Flash Adobe

Para cada anúncio complementar, o TVSDK indica quais tipos estão disponíveis para seu aplicativo.

1. Adicione um ouvinte para o evento `AdPlaybackEventListener.onAdBreakStart` que faz o seguinte:

   * Apaga anúncios existentes na instância do banner.
   * Obtém a lista de anúncios complementares de `Ad.getCompanionAssets`.
   * Se a lista de anúncios complementares não estiver vazia, passe o mouse sobre a lista para as instâncias de banner.

      Cada instância de banner (um `AdAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
   * Se um anúncio de vídeo não tiver anúncios complementares reservados, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.
   * Para mostrar um anúncio de exibição independente, adicione a lógica ao script para executar uma tag de anúncio de exibição DFP normal (DoubleClick for Publishers) na instância apropriada do banner.
   * Envia as informações do banner para uma função na página que exibe os banners em um local apropriado.

      Geralmente é um `div`, e sua função usa o `div ID` para exibir o banner.

