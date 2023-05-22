---
title: Criar um manipulador DRMStatusEvent
description: Criar um manipulador DRMStatusEvent
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Criar um manipulador DRMStatusEvent{#create-a-drmstatusevent-handler}

O exemplo a seguir cria um manipulador de eventos que gera as informações de status do conteúdo DRM para o objeto Primetime que originou o evento.

Adicione um manipulador de eventos a um objeto do Primetime que aponte para um conteúdo protegido:

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

