---
title: Criar um manipulador DRMErrorEvent
description: Criar um manipulador DRMErrorEvent
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Criar um manipulador DRMErrorEvent{#create-a-drmerrorevent-handler}

Crie um manipulador de eventos para processar eventos de erro despachados do Primetime quando ele encontrar um erro ao tentar reproduzir conteúdo protegido.

Normalmente, quando um aplicativo encontra um erro, ele executa qualquer número de tarefas de limpeza. Em seguida, ele informa o usuário sobre o erro e fornece opções para resolver o problema.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

