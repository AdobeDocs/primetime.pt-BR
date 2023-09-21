---
title: Casos de uso especiais
description: Casos de uso especiais
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Casos de uso especiais{#special-use-cases}

O TVSDK favorece configurações de intervalo personalizadas em relação às configurações de anúncio padrão. Por exemplo, se os intervalos MARK estiverem definidos, as configurações de inserção do anúncio serão ignoradas. Se os intervalos REPLACE estiverem definidos, o TVSDK usará automaticamente a variável `CustomRanges` modo de sinalização.

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

1. MARCAR e intervalos de DELETE com duração de substituição

   A duração de substituição extra é ignorada.
