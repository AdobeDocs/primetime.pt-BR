---
description: Os fluxos de mídia podem conter metadados adicionais na forma de tags no arquivo MPD (Media Presentation Description) e esse arquivo indica o posicionamento da publicidade. Você pode especificar nomes de tags personalizadas e ser notificado quando determinadas tags forem exibidas no arquivo de manifesto.
title: Tags personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# Visão geral {#custom-tags-overview}

Os fluxos de mídia podem conter metadados adicionais na forma de tags no arquivo MPD (Media Presentation Description) e esse arquivo indica o posicionamento da publicidade. Você pode especificar nomes de tags personalizadas e ser notificado quando determinadas tags forem exibidas no arquivo de manifesto.

## Tags de conteúdo HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Esse recurso não está disponível para o Safari em computadores da Apple, pois o TVSDK do navegador usa a tag de vídeo, em vez de Flash ou MSE, para reproduzir conteúdo HLS.

O TVSDK do navegador fornece suporte pronto para uso para tags de publicidade #EXT específicas. Seu aplicativo pode usar tags personalizadas para aprimorar o fluxo de trabalho de publicidade ou oferecer suporte a cenários de blecaute. Para suportar fluxos de trabalho avançados, o TVSDK do navegador permite que você especifique e assine tags adicionais no manifesto. Você pode ser notificado quando essas tags forem exibidas no arquivo de manifesto.

>[!TIP]
>
>Você pode assinar tags personalizadas para fluxos VOD e live/lineares.

>[!NOTE]
>
>Quando o HLS é reproduzido usando a tag Vídeo no Safari e não usando o Fallback do Flash, esse recurso não estará disponível no Safari.

## Uso de tags HLS personalizadas {#section_AD032318AEF5418393D2B1DF36B0BABB}

Veja um exemplo de um ativo VOD personalizado:

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

* Uma notificação quando `#EXT-X-ASSET` tags, ou qualquer outro conjunto de nomes de tags personalizados que você assinou, existem no arquivo.
* Insira anúncios quando uma tag `#EXT-X-AD` ou qualquer outro nome de tag personalizada for encontrada no fluxo.

Você pode assinar qualquer uma das seguintes tags como tags personalizadas: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. Você é notificado com um evento `TimedMetadata` durante a análise de arquivos de manifesto.

Há algumas tags de publicidade, como `EXT-X-CUE`, nas quais você já está inscrito. Essas tags de publicidade também são usadas pelo gerador de oportunidades padrão. Você pode especificar quais tags de publicidade são usadas pelo gerador de oportunidades padrão, definindo a propriedade `adTags` .

## Tags de conteúdo DASH {#section_967A952319BE4048B4C6612FFF7ADA6E}

O DASH tem duas maneiras de sinalizar eventos:

* No arquivo MPD.

   Esse arquivo é semelhante ao arquivo M3U8 no conteúdo HLS, e os eventos MPD existem no arquivo .mpd.
* Em banda na representação

   Os eventos em banda são multiplexados com representações adicionando as mensagens de evento como parte dos segmentos. Uma representação é uma lista de segmentos de vídeo e áudio que são reproduzidos em sequência. Os dados de evento em banda são incorporados nesses segmentos.

Esses eventos são notificados como `TimedMetadata` eventos ao aplicativo assim que forem analisados pelo TVSDK do navegador. Depois que um evento é notificado, ele não será notificado novamente.
