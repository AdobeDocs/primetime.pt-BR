---
description: É possível inserir anúncios no conteúdo de VOD.
title: Substituir intervalos de tempo por um anúncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Substituir intervalos de tempo por um anúncio {#replace-time-ranges-with-an-ad}

É possível inserir anúncios no conteúdo de VOD.

A variável `TimeRanges` entre as `begin` e `end` in `localTime` são removidos da linha do tempo. Esses intervalos são substituídos por um `AdBreak` de `begin` para `begin+replaceDuration`. Se a variável `replacement-duration` não existe como parâmetro, o servidor faz a determinação no campo `Adbreak`.

>[!TIP]
>
>Você deve sempre fornecer um `replacement-duration` para intervalos personalizados. Se nenhum anúncio tiver a intenção de substituir esse intervalo personalizado, forneça uma `replacement-duration` de 0.

1. Para substituir os intervalos pelos anúncios de Primetime e de decisão:

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
