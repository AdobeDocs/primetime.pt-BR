---
seo-title: Exemplo de um ativo VOD personalizado
title: Exemplo de um ativo VOD personalizado
uuid: 1db76b3f-b57a-428a-b79f-d4657ded8391
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

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

