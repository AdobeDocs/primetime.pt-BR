---
description: Você pode inserir publicidades no conteúdo VOD.
seo-description: Você pode inserir publicidades no conteúdo VOD.
seo-title: Substituir intervalos de tempo por um anúncio
title: Substituir intervalos de tempo por um anúncio
uuid: 50cdcc06-7df5-414b-95d4-c684bc68dce3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Substitua os intervalos de tempo por um anúncio{#replace-time-ranges-with-an-ad}

Você pode inserir publicidades no conteúdo VOD.

Nesse caso, `TimeRanges` entre `begin` e `end` em `localTime` são removidos da linha do tempo. Eles são substituídos por um `AdBreak` de `begin` para `begin+replaceDuration`. Se a substituição-duração não existir como parâmetro, o servidor faz a determinação no Adbreak retornado.

>[!NOTE]
>
>Você deve sempre fornecer uma duração de substituição específica para intervalos personalizados. Se nenhum anúncio for destinado a substituir esse intervalo personalizado, forneça uma duração de substituição de 0.

Substitua intervalos por anúncios de decisão do anúncio Primetime.

```
{   
    "properties": [],
    "stream": {
        "manifests": [ {
            "url": 
              "https://d398890tia84ty.cloudfront.net/e2e-vod/cloudfront_vod_hls_tos_30fps.m3u8",
            "type": "hls"
        } ],
                 
        "metadata": {
            "time-ranges": {
                "type": "replace",
                "time-range-list": [ {
                    "begin": 0,
                    "end": 15000,
                    "replacement-duration": 15000 
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

