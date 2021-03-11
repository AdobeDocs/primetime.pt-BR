---
description: O TVSDK prepara objetos TimedMetadata para as tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.
title: Assinar tags personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# Assinar tags personalizadas {#subscribe-to-custom-tags}

O TVSDK prepara objetos TimedMetadata para as tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.

Antes de a reprodução começar, você deve assinar as tags . Para ser notificado sobre tags personalizadas em manifestos de HLS:

1. Defina os nomes personalizados das tags de publicidade globalmente, transmitindo uma matriz que contenha as tags personalizadas para `setSubscribedTags` em `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Você deve incluir o prefixo `#` ao trabalhar com fluxos HLS.

   Por exemplo:

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
