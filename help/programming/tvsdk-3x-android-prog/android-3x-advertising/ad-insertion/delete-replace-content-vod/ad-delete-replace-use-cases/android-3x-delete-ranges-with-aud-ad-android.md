---
description: Você pode remover TimeRanges entre o início e o fim em localTime da linha do tempo.
seo-description: Você pode remover TimeRanges entre o início e o fim em localTime da linha do tempo.
seo-title: Excluir intervalos
title: Excluir intervalos
uuid: 2aaea7a0-5d52-49a1-901c-f71e4b081d91
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Excluir intervalos {#delete-ranges}

Você pode remover `TimeRanges` entre `begin` e `end` em `localTime` da linha do tempo.

>[!TIP]
>
>Para remover apenas determinados intervalos do conteúdo, crie uma instância `CustomRangeMetadata` e especifique o tipo como uma operação `DELETE` com os intervalos personalizados definidos.

O mapa de anúncios deve ser usado conforme definido pelo servidor de anúncios.

1. Para excluir intervalos com um anúncio de decisão de anúncio do Adobe Primetime:

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
