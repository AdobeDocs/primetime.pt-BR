---
description: Você pode remover TimeRanges entre o início e o fim em localTime da linha do tempo.
seo-description: Você pode remover TimeRanges entre o início e o fim em localTime da linha do tempo.
seo-title: Excluir intervalos
title: Excluir intervalos
uuid: 637829a7-efa8-4b83-9a04-ef01c043621f
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Excluir intervalos{#delete-ranges}

Você pode remover TimeRanges entre o início e o fim em localTime da linha do tempo.

>[!TIP]
>
>Para remover apenas determinados intervalos do conteúdo, crie uma `CustomRangeMetadata` instância e especifique o tipo como uma `DELETE` operação com os intervalos personalizados definidos.

O mapa de anúncios deve ser usado conforme definido pelo servidor de anúncios.

1. Para excluir intervalos com um anúncio de decisão do Adobe Primetime:

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
                   "type": "delete",
                   "time-range-list": [
                       {
                           "begin": 0,
                           "end": 20000
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
       "title": "VOD - DELETE TimeRange with xm-replace_text Phrase Ads",
       "thumbnail": {
           "large": "https://example.com",
           "small": "https://example.com"
       },
       "type": "vod",
       "id": "vod_003"
   },
   ```

