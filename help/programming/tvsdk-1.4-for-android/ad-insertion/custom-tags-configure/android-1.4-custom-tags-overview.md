---
title: Exemplo de um ativo VOD personalizado
description: Exemplo de um ativo VOD personalizado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Exemplo de um ativo VOD personalizado{#example-of-a-customized-vod-asset}

Veja um exemplo de um ativo VOD personalizado:

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

* Uma notificação quando `#EXT-X-ASSET` tags, ou qualquer outro conjunto de nomes de tags personalizados que você assinou, existem no arquivo.
* Insira anúncios quando uma tag `#EXT-X-AD` ou qualquer outro nome de tag personalizada for encontrada no fluxo.

