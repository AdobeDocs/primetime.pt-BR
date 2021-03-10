---
description: Você pode inserir anúncios no conteúdo VOD.
title: Substituir intervalos de tempo por um anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Substituir intervalos de tempo por um anúncio{#replace-time-ranges-with-an-ad}

Você pode inserir anúncios no conteúdo VOD.

Nesse caso, `TimeRanges` entre `begin` e `end` em `localTime` são removidas da linha do tempo. Eles são substituídos por um `AdBreak` de `begin` para `begin+replaceDuration`. Se a duração da substituição não existir como um parâmetro, o servidor fará a determinação no Adbreak retornado.

>[!NOTE]
>
>Você sempre deve fornecer uma duração de substituição específica para intervalos personalizados. Se nenhum anúncio tiver como objetivo substituir esse intervalo personalizado, forneça uma duração de substituição de 0.

Substitua os intervalos pelos anúncios de decisão do Primetime.

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

