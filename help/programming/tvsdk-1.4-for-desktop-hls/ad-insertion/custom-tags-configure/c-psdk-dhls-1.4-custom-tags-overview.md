---
title: Exemplo de um ativo de VOD personalizado
description: Exemplo de um ativo de VOD personalizado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Exemplo de um ativo de VOD personalizado{#example-of-a-customized-vod-asset}

Este é um exemplo de um ativo de VOD personalizado:

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

* Uma notificação quando `#EXT-X-ASSET` tags ou qualquer outro conjunto de nomes de tag personalizados que você tenha assinado existem no arquivo.
* Inserir anúncios quando um `#EXT-X-AD` tag, ou qualquer outro nome de tag personalizado, é encontrado no fluxo.
