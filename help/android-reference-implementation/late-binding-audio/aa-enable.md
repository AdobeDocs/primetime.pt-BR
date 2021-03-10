---
description: Você pode integrar fluxos de áudio de ligação tardia ou alternativos ao seu player criando um gerenciador de recursos de áudio alternativo.
title: Integrar áudio de ligação tardia
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Integrar áudio de ligação tardia {#integrate-late-binding-audio}

Você pode integrar fluxos de áudio de ligação tardia ou alternativos ao seu player criando um gerenciador de recursos de áudio alternativo.

* Para criar um gerenciador de áudio alternativo:

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* Para usar o ManagerFactory para ativar o áudio alternativo, verifique se a seguinte linha de código está no arquivo `PlayerFragment.java`:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   Para desativar o áudio alternativo:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

