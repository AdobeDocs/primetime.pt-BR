---
seo-title: Exemplo de um ativo VOD personalizado
title: Exemplo de um ativo VOD personalizado
uuid: 21e83b47-d7e2-4a2d-8a0b-80dd09e253a8
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Exemplo de um ativo VOD personalizado {#example-of-a-customized-vod-asset}

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

