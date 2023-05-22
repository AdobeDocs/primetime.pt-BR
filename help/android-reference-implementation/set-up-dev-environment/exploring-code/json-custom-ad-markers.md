---
title: Objeto JSON para marcadores de anúncios personalizados
description: Objeto JSON para marcadores de anúncios personalizados
copied-description: true
exl-id: 85bcf306-703c-4a0d-b125-df9316fadf69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Objeto JSON para marcadores de anúncios personalizados {#json-object-for-custom-ad-markers}

O bloco de código abaixo define o objeto JSON &quot;detalhes&quot; quando o tipo é marcadores de anúncio personalizados.

O MetadataNode retornado por IFeedItemAdapter:getStreamMetadata() contém duas entradas:
1. uma entrada com chave do tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` e o valor de uma instância de MetadataNode retornada por `TimeRangeCollection.toMetadata()`.
1. A segunda entrada tem uma chave do tipo `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` com o valor de *ajustar-buscar-posição* atributo abaixo.

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
| ajustar-buscar-posição | true ou false, usado para definir o valor da chave com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED no MetadataNode. |
| intervalos de tempo | Uma matriz de objetos JSON que indica o intervalo de tempo para cada marcador de anúncio. Cada entrada de Objeto JSON mapeia para uma instância de com.adobe.mediacore.utils.TimeRange. |
| time-ranges.begin | Valor em ms indicando a hora inicial do marcador de anúncio. |
| time-ranges.end | Valor em ms indicando a hora final do marcador de anúncio. |

Consulte a documentação do TVSDK para obter mais informações sobre como os marcadores de anúncios personalizados funcionam.
