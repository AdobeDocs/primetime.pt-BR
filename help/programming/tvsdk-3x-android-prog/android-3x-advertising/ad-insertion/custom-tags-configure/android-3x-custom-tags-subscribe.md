---
description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-title: Assinar tags personalizadas
title: Assinar tags personalizadas
uuid: f1a934bd-772e-435f-84b5-cb48db23c06e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Assinar tags personalizadas {#subscribe-to-custom-tags}

O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.

Antes do início da reprodução, você deve assinar as tags. Para ser notificado sobre tags personalizadas em manifestos HLS:

1. Defina os nomes personalizados das tags de publicidade globalmente, transmitindo uma matriz que contenha as tags personalizadas para `setSubscribedTags` o `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Você deve incluir o `#` prefixo ao trabalhar com fluxos HLS.

   Por exemplo:

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```
