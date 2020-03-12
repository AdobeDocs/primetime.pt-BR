---
seo-title: Objeto JSON para anúncios do Primetime
title: Objeto JSON para anúncios do Primetime
uuid: acf968d2-9856-4ed6-a046-1ac17d176571
description: O bloco de código abaixo define os detalhes do objeto JSON quando o valor do tipo é Anúncios Primetime.
seo-description: O bloco de código abaixo define os detalhes do objeto JSON quando o valor do tipo é Anúncios Primetime.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Objeto JSON para anúncios do Primetime {#json-object-for-primetime-ads}

O bloco de código abaixo define os detalhes do objeto JSON quando o valor do tipo é Anúncios Primetime.

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
| domínio | O domínio de anúncios Primetime a ser usado para solicitações de anúncios. |
| mediaid | O mediaid que foi configurado nos anúncios do Primetime para esse conteúdo. |
| zoneid | O Primetime adiciona zoneid. Consulte a documentação dos anúncios do Primetime para obter mais informações. |
| definição | Uma matriz de pares de chave/valor usados para direcionar anúncios específicos para o conteúdo. |

Consulte [com.adobe.mediacore.metadata.AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/metadata/AuditudeSettings.html) para obter mais informações sobre o valor desses atributos.