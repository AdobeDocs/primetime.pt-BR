---
description: Um anúncio pode ter vários elementos criativos, dos quais um é selecionado para ser reproduzido.
title: Tipos MIME válidos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Tipos MIME válidos{#valid-mime-types}

Um anúncio pode ter vários elementos criativos, dos quais um é selecionado para ser reproduzido.

Com tipos MIME, você pode especificar quais tipos de criação os usuários podem priorizar. Os tipos MIME especificados pelos usuários e os tipos MIME compatíveis com o TVSDK do navegador são usados para determinar qual criação será priorizada.

Para definir os tipos MIME válidos no TVSDK do navegador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

onde `mimeTypes` é uma matriz de cadeias de caracteres, e cada cadeia representa um tipo mime.

Caso vários arquivos de mídia sejam retornados para um anúncio, a seleção dependerá da ordem em que os arquivos de mídia aparecem no `validMimeTypes` matriz. Os tipos MIME que têm índice mais baixo têm preferência sobre aqueles com índice mais alto.
