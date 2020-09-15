---
description: Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar empacotar novamente anúncios incompatíveis em vídeos compatíveis do M3U8.
seo-description: Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar empacotar novamente anúncios incompatíveis em vídeos compatíveis do M3U8.
seo-title: Reempacotar anúncios incompatíveis usando o CRS (Adobe Creative Repacking Service)
title: Reempacotar anúncios incompatíveis usando o CRS (Adobe Creative Repacking Service)
uuid: ef542d13-6d52-4429-8a1e-0af2df236f12
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Reempacotar anúncios incompatíveis usando o CRS (Adobe Creative Repacking Service) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Alguns anúncios de terceiros (ou anúncios criativos) não podem ser associados ao fluxo de conteúdo HTTP Live Streaming (HLS) porque seu formato de vídeo é incompatível com HLS. Como opção, a inserção do anúncio Primetime e o TVSDK podem tentar empacotar novamente anúncios incompatíveis em vídeos compatíveis do M3U8.

Os anúncios veiculados de vários terceiros, como um servidor de agência, seu parceiro de inventário ou uma rede de anúncios, geralmente são veiculados em formatos incompatíveis, como o formato de download progressivo MP4.

Quando o TVSDK encontra um anúncio incompatível pela primeira vez, o player ignora o anúncio e emite uma solicitação para o serviço de reempacotamento de anúncios (CRS), que faz parte do back-end de inserção de anúncios do Primetime, para reempacotar o anúncio em um formato compatível. O CRS tenta gerar execuções de vários bits M3U8 do anúncio e armazena essas execuções no Primetime Content Delivery Network (CDN). Na próxima vez que o TVSDK receber uma resposta de anúncio que aponte para esse anúncio, o player usará a versão M3U8 compatível com HLS do CDN.

Para ativar este recurso CRS opcional, entre em contato com seu representante de Adobe.

>[!NOTE]
>
>Para clientes CRS versão 3.0 (e anteriores), a partir do CRS versão 3.1, as seguintes alterações melhoraram a segurança e o desempenho:
>
>* O CRS 3.1 continua com `https:` se o conteúdo que está sendo reempacotado usa `https:`. Isso reduz a possibilidade de alguns players apresentarem conteúdo inseguro.
   >
   >
* O CRS 3.1 minimiza muito as chamadas de rede, melhorando o tempo de inicialização do vídeo.

>



Para obter mais informações sobre o CRS, consulte [Creative Packaging Service (CRS)](../../../../../dynamic-ad-insertion/creative-repackaging-service/crs-overview.md).

## Habilitar CRS em aplicativos TVSDK {#enable-crs-in-tvsdk-applications}

Para ativar o CRS nos aplicativos TVSDK, você deve definir as seguintes informações nas configurações do Auditude:

1. Ative o CRS na `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
