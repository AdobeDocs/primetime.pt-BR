---
description: Você pode inserir anúncios no conteúdo VOD.
title: Substituir intervalos de tempo por um anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Substitua os intervalos de tempo por um anúncio {#replace-time-ranges-with-an-ad}

Você pode inserir anúncios no conteúdo VOD.

Os `TimeRanges` entre `begin` e `end` em `localTime` são removidos da linha do tempo. Esses intervalos são substituídos por um `AdBreak` de `begin` a `begin+replaceDuration`. Se `replacement-duration` não existir como um parâmetro, o servidor faz a determinação no `Adbreak` retornado.

>[!TIP]
>
>Você sempre deve fornecer um `replacement-duration` para intervalos personalizados. Se nenhum anúncio tiver como objetivo substituir esse intervalo personalizado, forneça um `replacement-duration` de 0.

1. Para substituir os intervalos pelos anúncios de decisão do Primetime ad:

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [
               {
                   "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
                   "type": "hls"
               }
           ],
           "metadata": {
               "time-ranges": {
                   "type": "replace",
                   "time-range-list": [
                       {
                           "begin": 0,
                           "end": 15000,
                           "replacement-duration": 15000
                       },
                       {
                                "begin": 69000,
                                "end": 99000,
                                "replacement-duration": 30000
                       },
                       {
                           "begin": 251000,
                           "end": 281000,
                           "replacement-duration": 30000
                       },
                       {
                           "begin": 514000,
                           "end": 544000,
                           "replacement-duration": 30000
                       }
                   ]
               },
               "ad": {
                   "targeting": [
                       {
                           "value": "MulAdsAvail12346",
                           "key": "osmfKeyMulAdsAvail12346"
                       }
                   ],
               "domain": "sandbox2.auditude.com",
               "mediaid": "psdk_000105",
               "zoneid": "121781"
               }     
           }
       },   
       "title": "VOD - Replace TimeRange with Auditude Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   }
   ```
