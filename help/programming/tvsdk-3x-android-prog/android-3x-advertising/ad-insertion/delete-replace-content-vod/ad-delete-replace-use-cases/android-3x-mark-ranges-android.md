---
description: Você pode designar intervalos de tempo no conteúdo VOD como intervalos de anúncio.
seo-description: Você pode designar intervalos de tempo no conteúdo VOD como intervalos de anúncio.
seo-title: Marcar intervalos
title: Marcar intervalos
uuid: fa6047dc-9a12-42fa-9e58-8ee3a55fa866
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Marcar intervalos {#mark-ranges}

Você pode designar intervalos de tempo no conteúdo VOD como intervalos de anúncio.

O `TimeRanges` entre `begin` e `end` em `localTime` será marcado como um `AdBreak` na linha do tempo. Outras configurações de publicidade são ignoradas.

>[!TIP]
>
>Se você quiser marcar apenas determinados intervalos no conteúdo como anúncios, sem inserir anúncios dinâmicos, crie uma instância `CustomRangeMetadata` e especifique o tipo como uma operação `MARK` com os intervalos personalizados definidos.

1. Marque os intervalos com a marca Tp:

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
                   "type": "mark",
               "adjust-seek-position" : true,   
                   "time-range-list": [
                     {
                        "begin": 0,
                        "end": 15000
                       },
                     {
                        "begin": 69000,
                        "end": 99000
                       },
                     {
                         "begin": 251000,
                         "end": 281000
                       },
                     {
                         "begin": 514000,
                         "end": 544000
                       }
                    ]
   
                 }
            }           
       },   
       "title": "VOD - MARK TimeRanges and no ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
          },
       "type": "vod",
       "id": "vod_004"
   }
   ```
