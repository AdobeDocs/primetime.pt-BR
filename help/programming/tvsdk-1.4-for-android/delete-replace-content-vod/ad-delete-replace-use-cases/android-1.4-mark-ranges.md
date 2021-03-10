---
description: Você pode designar intervalos de tempo no conteúdo VOD como ad breaks.
title: Marcar intervalos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Marcar intervalos{#mark-ranges}

Você pode designar intervalos de tempo no conteúdo VOD como ad breaks.

Nesse caso, `TimeRanges` entre `begin` e `end` em `localTime` será marcado como `AdBreak` na linha do tempo. Outras configurações de anúncio são ignoradas.

>[!NOTE]
>
>Se desejar marcar apenas determinados intervalos no conteúdo como anúncios (sem inserção dinâmica de anúncio), crie uma instância `CustomRangeMetadata` e especifique o tipo como uma operação MARK com os intervalos personalizados definidos.

1. Marcar intervalos.

   ```
   {   
       "properties": [],
       "stream": {
           "manifests": [ {
               "url": "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
               "type": "hls"
           } ],
           "metadata": {
               "time-ranges": {
                   "type": "mark",
                   "adjust-seek-position" : true,   
                   "time-range-list": [ {
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
                    } ]
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

