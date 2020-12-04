---
seo-title: Criar um manipulador DRMStatusEvent
title: Criar um manipulador DRMStatusEvent
uuid: 64f539d9-344c-4372-88b8-c8d098af9dd8
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Criar um manipulador DRMStatusEvent{#create-a-drmstatusevent-handler}

O exemplo a seguir cria um manipulador de eventos que gera as informações de status do conteúdo DRM para o objeto Primetime que originou o evento.

Adicione um manipulador de eventos a um objeto Primetime que aponte para conteúdo protegido:

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

