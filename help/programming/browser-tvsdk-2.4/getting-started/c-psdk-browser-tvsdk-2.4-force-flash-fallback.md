---
description: O sinalizador forceflash na lista de origem força o fallback do Flash para um URL. Para este URL, você pode usar o Adobe Flash Player para reproduzir o conteúdo.
title: Forçar o fallback do Flash usando a lista de fonte de mídia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# Forçar o fallback do Flash usando a lista de origem de mídia{#forcing-the-flash-fallback-using-the-media-source-list}

O sinalizador forceflash na lista de origem força o fallback do Flash para um URL. Para este URL, você pode usar o Adobe Flash Player para reproduzir o conteúdo.

Na lista de origem da mídia (por exemplo, no arquivo `sources.js`), você pode definir `forceflash` como `true`. Por exemplo:

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

