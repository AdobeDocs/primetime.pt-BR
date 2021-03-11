---
keywords: setSecure;VideoEngineView
title: Ativar captura de tela
description: Ativar captura de tela
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Ativar captura de tela{#enable-screen-capture}

O TVSDK não permite captura de tela por padrão. O reprodutor chama `setSecure(true)` no objeto `com.adobe.ave.VideoEngineView` no momento da construção. Você tem acesso a esse objeto, pois precisa construir um objeto `VideoEngineView` e fornecê-lo ao objeto `VideoEngine`.

Para ativar a captura de tela no aplicativo:

1. Construa o objeto `com.adobe.ave.VideoEngineView`.
1. Chame `setSecure(false)` no objeto `VideoEngineView`.
