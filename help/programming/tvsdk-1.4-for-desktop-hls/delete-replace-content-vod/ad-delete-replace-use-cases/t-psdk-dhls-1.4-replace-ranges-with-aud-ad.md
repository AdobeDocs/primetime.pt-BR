---
title: Substitua os intervalos de tempo por um anúncio de decisão de anúncio do Adobe Primetime
description: Substitua os intervalos de tempo por um anúncio de decisão de anúncio do Adobe Primetime
copied-description: true
exl-id: 263274b7-4602-4be0-b0ad-040f6f0f2fae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# Substitua os intervalos de tempo por um anúncio de decisão de anúncio do Adobe Primetime{#replace-time-ranges-with-an-adobe-primetime-ad-decisioning-ad}

Remover `TimeRanges` entre as `begin` e `end` in `localTime` da linha do tempo. Substituir por um AdBreak de `begin` para `begin+replaceDuration`.

Substitua os intervalos com anúncios do Primetime e do Decisioning.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": "https://. . ./cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replace-duration": 15000
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
                } ]

            },
            "ad": {
                "targeting": [ {
                    "value": "MulAdsAvail12346",
                    "key": "osmfKeyMulAdsAvail12346"
                } ],
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
