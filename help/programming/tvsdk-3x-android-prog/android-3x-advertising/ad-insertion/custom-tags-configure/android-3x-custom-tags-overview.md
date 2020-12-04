---
seo-title: Exemplo de um ativo VOD personalizado
title: Exemplo de um ativo VOD personalizado
uuid: 25927d5f-ac16-45f4-bf0d-92f1ab394c05
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Exemplo de um ativo VOD personalizado{#example-of-a-customized-vod-asset}

Este é um exemplo de um ativo VOD personalizado:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

Seu aplicativo pode configurar os seguintes cenários:

* Uma notificação quando as tags `#EXT-X-ASSET`, ou qualquer outro conjunto de nomes de tags personalizadas que você assinou, existem no arquivo.
* Insira publicidades quando uma tag `#EXT-X-AD`, ou qualquer outro nome de tag personalizado, for encontrada no fluxo.

