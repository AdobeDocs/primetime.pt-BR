---
description: O sinalizador forceflash na lista de origem força o fallback do Flash para um URL. Nesse URL, você pode usar o Adobe Flash Player para reproduzir o conteúdo.
title: Forçar o fallback do Flash usando a lista de origem de mídia
exl-id: 657bf9b1-d911-489d-80ca-2956b008431b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Forçar o fallback do Flash usando a lista de origem de mídia{#forcing-the-flash-fallback-using-the-media-source-list}

O sinalizador forceflash na lista de origem força o fallback do Flash para um URL. Nesse URL, você pode usar o Adobe Flash Player para reproduzir o conteúdo.

Na lista de origem da mídia (por exemplo, na caixa `sources.js` arquivo), você pode definir `forceflash` para `true`. Por exemplo:

```js
{ 
        "title":"Title of the item listed in the media source list",
        "description":"Description of the item listed in the media source list",
        "isLive":true,
        "content":[ 
            { 
                "format":"HLS",
                "url":"https://path_to_HLS_stream.m3u8"
            },
 
        ],
        "forceflash" : true
},
```
