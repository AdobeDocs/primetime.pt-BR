---
title: Objeto JSON para quebras diretas de anúncios
description: Detalha o objeto JSON quando o valor do tipo é direto e quebra
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Objeto JSON para quebras de anúncio direto{#json-object-for-direct-ad-breaks}

O bloco de código a seguir define os detalhes do objeto JSON quando o valor do tipo é ad breaks diretos.

O `MetadataNode` retornado por `IFeedItemAdapter:getStreamMetadata()` contém uma entrada com chave do tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` e o valor de uma representação de string do valor de objeto JSON de detalhes abaixo.

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
| `tag` | Uma string que mapeia para o campo de tag em `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `time` | Indica a hora de início do ad break, mapeia para o campo de hora em `com.adobe.mediacore.timeline.advertising.AdBreak`. Um valor de 0 indica um anúncio precedente. |
| `replace` | Indica a duração da substituição do ad break, mapeia para o campo `replaceDuration` em `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Uma lista de anúncios a serem reproduzidos durante o ad break fornecido mapeia para o campo `List<Ad>` em `com.adobe.mediacore.timeline.advertising.AdBreak`. |

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
| `url` | O URL para o conteúdo do anúncio mapeia para o campo de url em `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | A duração do anúncio é mapeada para o campo de duração em `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | Uma string de descrição. |

