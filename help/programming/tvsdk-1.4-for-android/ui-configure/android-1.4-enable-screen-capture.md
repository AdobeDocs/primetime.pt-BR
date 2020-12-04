---
description: nulo
keywords: setSecure;VideoEngineView
seo-description: nulo
seo-title: Ativar captura de tela
title: Ativar captura de tela
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# Ativar captura de tela{#enable-screen-capture}

O TVSDK não permite a captura de tela por padrão. O player chama `setSecure(true)` no objeto `com.adobe.ave.VideoEngineView` no momento da construção. Você tem acesso a esse objeto, pois precisa construir um objeto `VideoEngineView` e fornecê-lo ao objeto `VideoEngine`.

Para ativar a captura de tela no aplicativo:

1. Construa o objeto `com.adobe.ave.VideoEngineView`.
1. Chame `setSecure(false)` no objeto `VideoEngineView`.
