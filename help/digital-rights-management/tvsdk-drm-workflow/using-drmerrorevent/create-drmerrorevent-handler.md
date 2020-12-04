---
seo-title: Criar um manipulador DRMErrorEvent
title: Criar um manipulador DRMErrorEvent
uuid: dde660fc-6899-47d4-97d4-46acda2db262
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Criar um manipulador DRMErrorEvent{#create-a-drmerrorevent-handler}

Crie um manipulador de eventos para processar eventos de erro despachados do Primetime quando ele encontrar um erro ao tentar reproduzir conteúdo protegido.

Normalmente, quando um aplicativo encontra um erro, ele executa qualquer número de tarefas de limpeza. Em seguida, informa o usuário do erro e fornece opções para resolver o problema.

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

