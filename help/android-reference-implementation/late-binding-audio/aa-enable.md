---
description: É possível integrar fluxos de áudio alternativos ou de associação tardia ao player criando um gerenciador de recurso de áudio alternativo.
title: Integrar áudio de ligação tardia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Integrar áudio de ligação tardia {#integrate-late-binding-audio}

É possível integrar fluxos de áudio alternativos ou de associação tardia ao player criando um gerenciador de recurso de áudio alternativo.

* Para criar um gerenciador de áudio alternativo:

  ```java
  AAManager aaManager = new AAManagerOn(); 
  ```

* Para usar o ManagerFactory para ativar o áudio alternativo, verifique se a seguinte linha de código está no `PlayerFragment.java` arquivo:

  ```java
  aaManager = ManagerFactory.getAAManager( 
  <b>true</b>,config, mediaPlayer);
  ```

  Para desativar o áudio alternativo:

  ```java
  aaManager = ManagerFactory.getAAManager( 
  <b>false</b>,config, mediaPlayer);
  ```
