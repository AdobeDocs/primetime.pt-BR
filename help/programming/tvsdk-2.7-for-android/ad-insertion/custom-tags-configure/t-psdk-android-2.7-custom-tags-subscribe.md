---
description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-title: Assinar tags personalizadas
title: Assinar tags personalizadas
uuid: 9f74b2b9-bbc9-433c-8226-2c2b68eddf7e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

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

