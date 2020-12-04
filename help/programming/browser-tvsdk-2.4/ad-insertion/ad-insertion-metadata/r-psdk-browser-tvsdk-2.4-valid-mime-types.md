---
description: Um anúncio pode ter vários anúncios, dos quais um é selecionado para reprodução.
seo-description: Um anúncio pode ter vários anúncios, dos quais um é selecionado para reprodução.
seo-title: Tipos mime válidos
title: Tipos mime válidos
uuid: ab2baac9-a9ef-44f1-83a1-2e6e471e3231
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Tipos de mime válidos{#valid-mime-types}

Um anúncio pode ter vários anúncios, dos quais um é selecionado para reprodução.

Com tipos MIME, você pode especificar que tipo criativo os usuários podem priorizar. Os tipos mime especificados pelos usuários e os tipos mime compatíveis com o TVSDK do navegador são usados para determinar qual criação será priorizada.

Para definir os tipos MIME válidos no TVSDK do navegador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

em que `mimeTypes` é uma matriz de sequências de caracteres e cada string representa um tipo mime.

Caso vários arquivos de mídia sejam retornados para um anúncio, a seleção depende da ordem em que os arquivos de mídia aparecem na matriz `validMimeTypes`. Os tipos mime com índice mais baixo recebem preferência em relação aos com índice mais alto.
