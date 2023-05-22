---
keywords: setSecure;VideoEngineView
title: Habilitar captura de tela
description: Habilitar captura de tela
copied-description: true
exl-id: 5dd1bf4e-ab50-4b57-89e4-eacc291a9fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# Habilitar captura de tela{#enable-screen-capture}

O TVSDK não permite a captura de tela por padrão. O reprodutor chama `setSecure(true)` no `com.adobe.ave.VideoEngineView` objeto no momento da construção. Você tem acesso a esse objeto, pois precisa construir um `VideoEngineView` e forneça-o ao `VideoEngine` objeto.

Para ativar a captura de tela no aplicativo:

1. Construir o `com.adobe.ave.VideoEngineView` objeto.
1. Chame `setSecure(false)` no seu `VideoEngineView` objeto.
