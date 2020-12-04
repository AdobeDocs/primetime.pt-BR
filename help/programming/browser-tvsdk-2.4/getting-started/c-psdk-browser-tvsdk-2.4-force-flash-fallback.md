---
description: O sinalizador forceflash na lista de origem força o fallback do Flash para um URL. Para este URL, você pode usar o Adobe Flash Player para reproduzir o conteúdo.
seo-description: O sinalizador forceflash na lista de origem força o fallback do Flash para um URL. Para este URL, você pode usar o Adobe Flash Player para reproduzir o conteúdo.
seo-title: Forçar o fallback do Flash usando a lista de origem da mídia
title: Forçar o fallback do Flash usando a lista de origem da mídia
uuid: 04b09734-15f7-4e7e-8802-344f550f9b05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 1%

---


# Forçar o fallback do Flash usando a lista de origem de mídia{#forcing-the-flash-fallback-using-the-media-source-list}

O sinalizador forceflash na lista de origem força o fallback do Flash para um URL. Para este URL, você pode usar o Adobe Flash Player para reproduzir o conteúdo.

Na lista de origem de mídia (por exemplo, no arquivo `sources.js`), você pode definir `forceflash` como `true`. Por exemplo:

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

