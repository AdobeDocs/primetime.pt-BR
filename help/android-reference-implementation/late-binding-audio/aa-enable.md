---
description: É possível integrar fluxos de áudio alternativos ou de associação tardia ao player criando um gerenciador de recurso de áudio alternativo.
title: Integrar áudio de ligação tardia
exl-id: 43be9042-d547-4646-a920-cdd2a5dbb1fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
