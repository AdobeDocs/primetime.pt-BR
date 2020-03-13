---
description: nulo
seo-description: nulo
seo-title: Casos de uso especiais
title: Casos de uso especiais
uuid: 066bc256-4fdf-4083-b23e-0a916b3b532f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Casos de uso especiais{#special-use-cases}

O TVSDK favorece as configurações de intervalo personalizado em relação às configurações de anúncio padrão. Por exemplo, se os intervalos MARK estiverem definidos, as configurações de inserção do anúncio serão ignoradas. Se os intervalos REPLACE estiverem definidos, o TVSDK usará automaticamente o modo de `CustomRanges` sinalização.

1. `ReplaceRange` sem duração de substituição

   Se a duração da substituição estiver ausente, a duração real da substituição será determinada pelo servidor. O número de anúncios colocados nesse link também `AdBreak` é determinado pelo servidor.

   ```
   {
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://. . ./vanilla/index.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "signaling-mode": "custom time ranges",
               "time-ranges": {
                   "type": "replace",
                   "adjust-seek-position": true,
                   "time-range-list": [{
                   "begin": 0,
                   "end": 30000
               }, {
                   "begin": 60000,
                   "end": 75000
               }, {
                   "begin": 255000,
                   "end": 300000
               } ]
               },
               "ad": {             
                   "domain": "sandbox2.auditude.com",
                   "mediaid": "psdk_000105",
                   "zoneid": "121781"
               }     
           }
       },
       "title": "Verify 30Sec Pre-Roll, 15 Sec Mid roll Ad and 
       45 second Post-Roll can be replaced in one shot.",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_001"
   }
   ```

1. Intervalos MARK e DELETE com duração de substituição

   A duração extra de substituição é ignorada.
