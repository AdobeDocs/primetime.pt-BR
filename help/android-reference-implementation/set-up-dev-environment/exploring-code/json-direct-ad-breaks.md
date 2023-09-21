---
title: Objeto JSON para ad breaks diretos
description: Detalha o objeto JSON quando o valor do tipo é ad breaks diretos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Objeto JSON para ad breaks diretos{#json-object-for-direct-ad-breaks}

O bloco de código a seguir define o objeto JSON de detalhes quando o valor do tipo é ad breaks diretos.

A variável `MetadataNode` retornado por `IFeedItemAdapter:getStreamMetadata()` contém uma entrada com chave do tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` e o valor de uma representação da string do valor do objeto JSON de detalhes abaixo.

```
“metadata”: { 
    “ad” :  { 
        “type”: “direct ad breaks”, 
        “details”: { 
            "ad-breaks": [ 
                { 
                    "tag": "break-001", 
                    "time": 0, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        }, 
                        { 
                        } 
                    ] 
                }, 
                { 
                    "tag": "break-002", 
                    "time": 300000, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        } 
                    ] 
                } 
            ] 
        } 
    } 
} 
```

| Propriedade | Descrição |
|---|---|
| `tag` | Uma string que mapeia para o campo de tag no `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | Indica a hora de início do ad break, mapeia para o campo de hora em `com.adobe.mediacore.timeline.advertising.AdBreak`. O valor 0 indica um anúncio precedente. |
| `replace` | Indica a duração da substituição do ad break, mapeia para a variável `replaceDuration` campo em `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Uma lista de anúncios a serem reproduzidos durante o ad break, mapeia para o `List<Ad>` campo em `com.adobe.mediacore.timeline.advertising.AdBreak`. |

O bloco de código a seguir define o objeto JSON para a matriz da lista de anúncios.

```
"ad-list": [ 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 15000, 
        "tag": "1st break - 1st ad" 
    }, 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 30000, 
        "tag": "1st break - 2nd ad" 
    } 
], 
```

| Propriedade | Descrição |
|---|---|
| `url` | O URL para o conteúdo do anúncio mapeia para o campo URL no `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | A duração do anúncio é mapeada para o campo de duração em `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | Uma string de descrição. |
