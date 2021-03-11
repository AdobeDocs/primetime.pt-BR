---
title: Objeto JSON para marcadores de anúncio personalizados
description: Objeto JSON para marcadores de anúncio personalizados
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Objeto JSON para marcadores de anúncio personalizados {#json-object-for-custom-ad-markers}

O bloco de código abaixo define o objeto JSON de &quot;detalhes&quot; quando o tipo é marcadores de anúncio personalizados.

O MetadataNode retornado por IFeedItemAdapter:getStreamMetadata() contém 2 entradas:
1. uma entrada com chave do tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` e valor de uma instância do MetadataNode retornado por `TimeRangeCollection.toMetadata()`.
1. A segunda entrada tem uma chave do tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` com o valor do atributo *ajuste-busca-posição* abaixo.

```
“metadata”: {
    “ad” :  {
        “type”: “custom ad markers”,
        “details”: {
            "adjust-seek-position": true,
            "time-ranges": [
                {
                    "begin": 5000,
                    "end":15000
                },
                {
                    "begin": 120000,
                    "end":135000
                }
            ]
        }
    }
}
```

| Propriedade | Descrição |
|---|---|
| ajuste-busca-posição | verdadeiro ou falso, usado para definir o valor da chave com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED no MetadataNode. |
| intervalos de tempo | Uma matriz de objetos JSON que indica o intervalo de tempo para cada marcador de anúncio. Cada entrada de Objeto JSON mapeia para uma instância de com.adobe.mediacore.utils.TimeRange. |
| time-ranges.begin | Valor em ms que indica a hora de início do marcador de anúncio. |
| time-ranges.end | Valor em ms que indica a hora de término do marcador de anúncio. |

Consulte a documentação do TVSDK para obter mais informações sobre como os marcadores de anúncios personalizados funcionam.
