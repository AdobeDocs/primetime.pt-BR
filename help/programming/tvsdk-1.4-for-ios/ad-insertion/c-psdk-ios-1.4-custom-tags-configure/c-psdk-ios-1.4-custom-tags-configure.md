---
description: Os fluxos de mídia podem conter metadados adicionais na forma de tags na lista de reprodução/arquivo manifest, e esse arquivo indica a colocação de publicidade. Você pode especificar nomes de tags personalizadas e ser notificado quando determinadas tags forem exibidas no arquivo manifest.
seo-description: Os fluxos de mídia podem conter metadados adicionais na forma de tags na lista de reprodução/arquivo manifest, e esse arquivo indica a colocação de publicidade. Você pode especificar nomes de tags personalizadas e ser notificado quando determinadas tags forem exibidas no arquivo manifest.
seo-title: Tags personalizadas
title: Tags personalizadas
uuid: 0f47bed6-2ae8-4e4b-9f6f-672020dc3265
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Visão geral {#custom-tags-overview}

Os fluxos de mídia podem conter metadados adicionais na forma de tags na lista de reprodução/arquivo manifest, e esse arquivo indica a colocação de publicidade. Você pode especificar nomes de tags personalizadas e ser notificado quando determinadas tags forem exibidas no arquivo manifest.

## Tags de conteúdo HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Este recurso não está disponível para o Safari em computadores Apple, pois o TVSDK usa a tag de vídeo, em vez de Flash ou MSE, para reproduzir conteúdo HLS.

O TVSDK oferece suporte imediato para tags de publicidade #EXT específicas. Seu aplicativo pode usar tags personalizadas para aprimorar o fluxo de trabalho de publicidade ou para oferecer suporte a cenários de blecaute. Para suportar workflows avançados, o TVSDK permite que você especifique e assine tags adicionais no manifesto. Você pode ser notificado quando essas tags forem exibidas no arquivo manifest.

>[!TIP]
>
>Você pode assinar tags personalizadas para fluxos VOD e live/linear.

>[!NOTE]
>
>Quando o HLS é reproduzido usando a tag Vídeo no Safari, e não usando o recurso Flash Fallback, esse recurso não estará disponível no Safari.

## Usar tags HLS personalizadas {#section_AD032318AEF5418393D2B1DF36B0BABB}

Este é um exemplo de um ativo VOD personalizado:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

Seu aplicativo pode configurar os seguintes cenários:

* Uma notificação quando as tags `#EXT-X-ASSET`, ou qualquer outro conjunto de nomes de tags personalizadas que você assinou, existem no arquivo.
* Insira publicidades quando uma tag `#EXT-X-AD`, ou qualquer outro nome de tag personalizado, for encontrada no fluxo.

Você pode assinar qualquer uma das seguintes tags como tags personalizadas: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. Você é notificado com um evento `TimedMetadata` durante a análise de arquivos manifest.

Há algumas tags de publicidade, como `EXT-X-CUE`, nas quais você já está inscrito. Essas tags de publicidade também são usadas pelo gerador de oportunidades padrão. Você pode especificar quais tags de publicidade são usadas pelo gerador de oportunidades padrão, definindo a propriedade `adTags`.
