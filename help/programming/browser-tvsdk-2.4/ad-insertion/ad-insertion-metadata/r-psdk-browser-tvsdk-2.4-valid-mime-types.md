---
description: Um anúncio pode ter vários anúncios, dos quais um é selecionado para reprodução.
title: Tipos mime válidos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Tipos mime válidos{#valid-mime-types}

Um anúncio pode ter vários anúncios, dos quais um é selecionado para reprodução.

Com os tipos MIME, você pode especificar quais tipos de criação os usuários podem priorizar. Os tipos mime especificados pelos usuários e os tipos mime compatíveis com o TVSDK do navegador são usados para determinar qual criação será priorizada.

Para definir os tipos MIME válidos no Browser TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

onde `mimeTypes` é uma matriz de strings e cada string representa um tipo MIME.

Caso vários arquivos de mídia sejam retornados para um anúncio, a seleção depende da ordem em que os arquivos de mídia aparecem na matriz `validMimeTypes`. Os tipos mime que têm índice mais baixo recebem preferência em relação aos que têm índice mais alto.
