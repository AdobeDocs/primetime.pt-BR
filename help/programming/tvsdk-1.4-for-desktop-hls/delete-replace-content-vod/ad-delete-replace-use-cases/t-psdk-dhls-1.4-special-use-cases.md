---
title: Casos de uso especiais
description: Casos de uso especiais
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Casos de uso especiais{#special-use-cases}

O TVSDK favorece configurações de intervalo personalizadas em configurações de anúncios padrão. Por exemplo, se os intervalos MARK forem definidos, as configurações de inserção do anúncio serão ignoradas. Se os intervalos REPLACE forem definidos, o TVSDK usará automaticamente o modo de sinalização `CustomRanges`.

1. `ReplaceRange` sem duração de substituição

   Se a duração da substituição estiver ausente, a duração real da substituição será determinada pelo servidor. O número de anúncios colocados neste `AdBreak` também é determinado pelo servidor.

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
