---
keywords: setSecure;VideoEngineView
title: Habilitar captura de tela
description: Habilitar captura de tela
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Habilitar captura de tela{#enable-screen-capture}

O TVSDK não permite a captura de tela por padrão. O reprodutor chama `setSecure(true)` no `com.adobe.ave.VideoEngineView` objeto no momento da construção. Você tem acesso a esse objeto, pois precisa construir um `VideoEngineView` e forneça-o ao `VideoEngine` objeto.

Para ativar a captura de tela no aplicativo:

1. Construir o `com.adobe.ave.VideoEngineView` objeto.
1. Chame `setSecure(false)` no seu `VideoEngineView` objeto.
