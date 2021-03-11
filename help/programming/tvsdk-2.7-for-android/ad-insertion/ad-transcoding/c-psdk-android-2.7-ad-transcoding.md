---
description: Alguns anúncios de terceiros (ou criações) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção de anúncios do Primetime e o TVSDK podem tentar reempacotar anúncios incompatíveis em vídeos compatíveis com o M3U8.
title: Reempacotar anúncios incompatíveis usando o Adobe Creative Repackaging Service (CRS)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Reempacotar anúncios incompatíveis usando o Adobe Creative Repackaging Service (CRS) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Alguns anúncios de terceiros (ou criações) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção de anúncios do Primetime e o TVSDK podem tentar reempacotar anúncios incompatíveis em vídeos compatíveis com o M3U8.

Anúncios veiculados em vários terceiros, como uma agência e servidor, seu parceiro de inventário ou uma rede de anúncios, geralmente são entregues em formatos incompatíveis, como o download progressivo do formato MP4.

Quando o TVSDK encontra um anúncio incompatível pela primeira vez, o reprodutor ignora o anúncio e emite uma solicitação para o CRS (creative repackaging service), que faz parte do back-end de inserção de anúncio do Primetime, para reempacotar o anúncio em um formato compatível. O CRS tenta gerar várias representações M3U8 de taxa de bits do anúncio e armazena essas representações na Rede de entrega de conteúdo (CDN) do Primetime. Na próxima vez em que o TVSDK receber uma resposta de anúncio que aponte para esse anúncio, o reprodutor usará a versão M3U8 compatível com HLS da CDN.

Para ativar esse recurso CRS opcional, entre em contato com o representante do Adobe.

>[!NOTE]
>
>Para clientes CRS versão 3.0 (e anteriores), a partir da versão 3.1 do CRS, as seguintes alterações melhoraram a segurança e o desempenho:
>
>* O CRS 3.1 continua com `https:` se o conteúdo que está sendo reempacotado usar `https:`. Isso reduz a possibilidade de alguns players apresentarem conteúdo inseguro.
   >
   >
* O CRS 3.1 minimiza muito as chamadas de rede, melhorando o tempo de inicialização do vídeo.

>



Para obter mais informações sobre CRS, consulte [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_certificate_enrollment.pdf).

## Habilitar CRS em aplicativos TVSDK{#enable-crs-in-tvsdk-applications}

Para ativar o CRS em seus aplicativos TVSDK, você deve definir as seguintes informações nas configurações do Auditude:

1. Habilite o CRS em `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
