---
description: Você pode inserir publicidades no conteúdo VOD.
seo-description: Você pode inserir publicidades no conteúdo VOD.
seo-title: Substituir intervalos de tempo por um anúncio
title: Substituir intervalos de tempo por um anúncio
uuid: 8f09560c-bca3-4662-bc58-6c9cd0892476
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Substituir intervalos de tempo por um anúncio {#replace-time-ranges-with-an-ad}

Você pode inserir publicidades no conteúdo VOD.

Os `TimeRanges` intervalos entre `begin` e `end` dentro `localTime` são removidos da linha do tempo. Esses intervalos são substituídos por um `AdBreak` de `begin` a `begin+replaceDuration`. Se o parâmetro `replacement-duration` não existir, o servidor fará a determinação no parâmetro retornado `Adbreak`.

>[!TIP]
>
>Você deve sempre fornecer um intervalo `replacement-duration` personalizado. Se nenhum anúncio for destinado a substituir esse intervalo personalizado, forneça um valor `replacement-duration` de 0.

1. Para substituir os intervalos por anúncios de decisão do Primetime ad:

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

