---
description: Você pode remover TimeRanges entre o início e o fim em localTime da linha do tempo.
title: Excluir intervalos
exl-id: 1c0f7718-8a40-4fc8-b70b-f751d8ff40a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 0%

---

# Excluir intervalos{#delete-ranges}

Você pode remover TimeRanges entre o início e o fim em localTime da linha do tempo.

>[!NOTE]
>
>Se você quiser remover apenas determinados intervalos do conteúdo, e o mapa de anúncios deve ser usado conforme definido pelo servidor de anúncios, crie um `CustomRangeMetadata` e especifique o tipo como uma operação DELETE com os intervalos personalizados definidos.

Exclua intervalos com um anúncio do Adobe Primetime Ad Decisioning.

```
{   
    "properties": [],
    "stream": {
        "manifests": [
            {
                "url": "https://xyz.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
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
    "title": "VOD - DELETE TimeRange with Primetime ad decisioning Ads",
    "thumbnail": {
        "large": "https://example.com",
        "small": "https://example.com"
    },
    "type": "vod",
    "id": "vod_003"
}
```
