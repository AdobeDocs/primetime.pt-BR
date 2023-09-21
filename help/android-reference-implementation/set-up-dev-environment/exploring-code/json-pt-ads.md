---
title: Objeto JSON para anúncios do Primetime
description: O bloco de código abaixo define o objeto JSON de detalhes quando o valor do tipo é anúncios do Primetime.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Objeto JSON para anúncios do Primetime {#json-object-for-primetime-ads}

O bloco de código abaixo define o objeto JSON de detalhes quando o valor do tipo é anúncios do Primetime.

```
“metadata”: {
    “ad” :  {
        “type”: “Primetime ads”,
        “details”: {
            "domain": "sandbox2.auditude.com",
            "mediaid": "rom_asset_case_1",
            "zoneid": "109754",
            "targeting": [
                {
                    "key": "osmfKeyMulAdsAvail12346",
                    "value": "MulAdsAvail12346"
                }
            ]
        }
    }
}
```

| Propriedade | Descrição |
|---|---|
| domínio | O domínio de anúncios do Primetime a ser usado para solicitações de anúncios. |
| mediaid | A mídia configurada nos anúncios do Primetime para esse conteúdo. |
| zoneid | O Primetime adiciona zoneid. Consulte a documentação de anúncios do Primetime para obter mais informações. |
| direcionamento | Uma matriz de pares de chave/valor usados para direcionar anúncios específicos para o conteúdo. |

Consulte [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) para obter mais informações sobre o valor desses atributos.
