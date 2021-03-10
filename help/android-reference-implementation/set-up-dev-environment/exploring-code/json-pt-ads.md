---
title: Objeto JSON para anúncios do Primetime
description: O bloco de código abaixo define os detalhes do objeto JSON quando o valor do tipo é anúncios do Primetime.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Objeto JSON para anúncios do Primetime {#json-object-for-primetime-ads}

O bloco de código abaixo define os detalhes do objeto JSON quando o valor do tipo é anúncios do Primetime.

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
| domínio | O domínio de anúncios do Primetime a ser usado nas solicitações de anúncios. |
| mediaid | O mediaid que foi configurado nos anúncios do Primetime para esse conteúdo. |
| zoneid | O Primetime adiciona zoneid. Consulte a documentação dos anúncios do Primetime para obter mais informações. |
| direcionamento | Uma matriz de pares de chave/valor usados para direcionar anúncios específicos para o conteúdo. |

Consulte [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) para obter mais informações sobre o valor desses atributos.