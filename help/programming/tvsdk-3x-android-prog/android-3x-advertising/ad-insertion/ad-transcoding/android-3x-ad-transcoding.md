---
description: Alguns anúncios de terceiros (ou criativos) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. A inserção de anúncios do Primetime e o TVSDK podem, opcionalmente, tentar reempacotar anúncios incompatíveis em vídeos M3U8 compatíveis.
title: Reempacotar anúncios incompatíveis usando o CRS (Serviço de Reempacotamento Criativo) do Adobe
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Reempacotar anúncios incompatíveis usando o CRS (Serviço de Reempacotamento Criativo) do Adobe {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Alguns anúncios de terceiros (ou criativos) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. A inserção de anúncios do Primetime e o TVSDK podem, opcionalmente, tentar reempacotar anúncios incompatíveis em vídeos M3U8 compatíveis.

Anúncios veiculados por vários terceiros, como um servidor de publicidade de uma agência, um parceiro de inventário ou uma rede de publicidade, geralmente são entregues em formatos incompatíveis, como o formato MP4 de download progressivo.

Quando o TVSDK encontra um anúncio incompatível pela primeira vez, o reprodutor ignora o anúncio e emite uma solicitação para o serviço de reempacotamento criativo (CRS), que faz parte do back-end de inserção de anúncio do Primetime, para reempacotar o anúncio em um formato compatível. O CRS tenta gerar várias representações M3U8 de taxa de bits do anúncio e armazena essas representações na Rede de entrega de conteúdo (CDN) do Primetime. Na próxima vez que o TVSDK receber uma resposta de anúncio que aponta para esse anúncio, o reprodutor usará a versão M3U8 compatível com HLS do CDN.

Para ativar esse recurso opcional do CRS, entre em contato com o representante da Adobe.

>[!NOTE]
>
>Para clientes CRS versão 3.0 (e anteriores), a partir da CRS versão 3.1, as seguintes alterações melhoraram a segurança e o desempenho:
>
>* O CRS 3.1 continua com `https:` se o conteúdo que está sendo reempacotado usar `https:`. Isso reduz a possibilidade de alguns players apresentarem conteúdo não seguro.
>
>* O CRS 3.1 minimiza muito as chamadas de rede, melhorando o tempo de inicialização do vídeo.
>

## Habilitar CRS em aplicativos TVSDK {#enable-crs-in-tvsdk-applications}

Para habilitar o CRS nos aplicativos TVSDK, você deve definir as seguintes informações nas configurações de Auditude:

1. Ativar CRS no `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
