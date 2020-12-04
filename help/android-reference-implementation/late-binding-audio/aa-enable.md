---
description: É possível integrar fluxos de áudio de ligação tardia ou alternativos ao player, criando um gerenciador de recursos de áudio alternativo.
seo-description: É possível integrar fluxos de áudio de ligação tardia ou alternativos ao player, criando um gerenciador de recursos de áudio alternativo.
seo-title: Integrar áudio de ligação tardia
title: Integrar áudio de ligação tardia
uuid: cd2e259a-2af4-4d7b-a856-79bd087e8ca6
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Integrar áudio de ligação tardia {#integrate-late-binding-audio}

É possível integrar fluxos de áudio de ligação tardia ou alternativos ao player, criando um gerenciador de recursos de áudio alternativo.

* Para criar um gerenciador de áudio alternativo:

   ```java
   AAManager aaManager = new AAManagerOn(); 
   ```

* Para usar o ManagerFactory para habilitar áudio alternativo, verifique se a seguinte linha de código está no arquivo `PlayerFragment.java`:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>true</b>,config, mediaPlayer);
   ```

   Para desativar o áudio alternativo:

   ```java
   aaManager = ManagerFactory.getAAManager( 
   <b>false</b>,config, mediaPlayer);
   ```

