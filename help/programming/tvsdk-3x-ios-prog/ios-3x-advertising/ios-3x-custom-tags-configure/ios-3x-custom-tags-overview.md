---
title: Exemplo de um ativo de VOD personalizado
description: Exemplo de um ativo de VOD personalizado
copied-description: true
exl-id: c5722e1f-75f7-40b6-861c-bbe348e1183b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Exemplo de um ativo de VOD personalizado {#example-of-a-customized-vod-asset}

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
