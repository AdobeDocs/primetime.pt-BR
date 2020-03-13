---
seo-title: Objeto JSON para quebras de anúncio direto
title: Objeto JSON para quebras de anúncio direto
uuid: ffb901f4-0a8b-40fe-b6ba-5ffebc324cf2
description: Detalhes do objeto JSON quando o valor do tipo é direto e quebras
seo-description: Detalhes do objeto JSON quando o valor do tipo é direto e quebras
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Objeto JSON para quebras de anúncio direto{#json-object-for-direct-ad-breaks}

O bloco de código a seguir define os detalhes do objeto JSON quando o valor do tipo é quebras de anúncio diretas.

O `MetadataNode` retornado por `IFeedItemAdapter:getStreamMetadata()` contém uma entrada com a chave do tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` e valor de uma representação de string do valor detalhado do objeto JSON abaixo.

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
| `time` | Indica a hora de início do intervalo do anúncio, mapeia para o campo de hora em `com.adobe.mediacore.timeline.advertising.AdBreak`. Um valor de 0 indica um anúncio precedente. |
| `replace` | Indica a duração da substituição da quebra de anúncio, mapeia para o `replaceDuration` campo em `com.adobe.mediacore.timeline.advertising.AdBreak`. |
| `ad-list` | Uma lista de anúncios a serem reproduzidos durante o intervalo de anúncios fornecido mapeia para o `List<Ad>` campo em `com.adobe.mediacore.timeline.advertising.AdBreak`. |

O seguinte bloco de código define o objeto JSON para a matriz de lista de anúncios.

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
| `url` | O URL para o conteúdo do anúncio é mapeado para o campo url em `com.adobe.mediacore.timeline.advertising.Ad`. |
| `duration` | A duração do anúncio é mapeada para o campo de duração em `com.adobe.mediacore.timeline.advertising.Ad`. |
| `tag` | Uma string de descrição. |

