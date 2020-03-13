---
description: Você pode designar intervalos de tempo no conteúdo VOD como intervalos de anúncio.
seo-description: Você pode designar intervalos de tempo no conteúdo VOD como intervalos de anúncio.
seo-title: Marcar intervalos
title: Marcar intervalos
uuid: eb99a1c2-6c0c-40a4-bac2-98dce45acfad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Marcar intervalos{#mark-ranges}

Você pode designar intervalos de tempo no conteúdo VOD como intervalos de anúncio.

Nesse caso, `TimeRanges` entre o `begin` e `end` em `localTime` será marcado como um `AdBreak` na linha do tempo. Outras configurações de anúncio são ignoradas.

>[!NOTE]
>
>Se você quiser marcar apenas determinados intervalos no conteúdo como anúncios (sem inserção dinâmica de anúncios), crie uma `CustomRangeMetadata` instância e especifique o tipo como uma operação MARK com os intervalos personalizados definidos.

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

