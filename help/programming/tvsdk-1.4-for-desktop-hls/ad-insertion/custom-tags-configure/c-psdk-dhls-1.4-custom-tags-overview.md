---
seo-title: Exemplo de um ativo VOD personalizado
title: Exemplo de um ativo VOD personalizado
uuid: 599054c3-d6ef-4f85-9a0f-39c7e4f6ab24
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

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

* Uma notificação quando `#EXT-X-ASSET` as tags, ou qualquer outro conjunto de nomes de tags personalizadas aos quais você se inscreveu, existem no arquivo.
* Insira publicidades quando uma `#EXT-X-AD` tag, ou qualquer outro nome de tag personalizado, for encontrada no stream.

