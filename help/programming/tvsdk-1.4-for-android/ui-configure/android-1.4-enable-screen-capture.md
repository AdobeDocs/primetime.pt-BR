---
description: nulo
keywords: setSecure;VideoEngineView
seo-description: nulo
seo-title: Ativar captura de tela
title: Ativar captura de tela
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Ativar captura de tela{#enable-screen-capture}

O TVSDK não permite a captura de tela por padrão. O jogador liga `setSecure(true)` para o `com.adobe.ave.VideoEngineView` objeto no momento da construção. Você tem acesso a esse objeto, pois precisa construir um `VideoEngineView` objeto e fornecê-lo ao `VideoEngine` objeto.

Para ativar a captura de tela no aplicativo:

1. Construa o `com.adobe.ave.VideoEngineView` objeto.
1. Chame `setSecure(false)` o seu `VideoEngineView` objeto.
