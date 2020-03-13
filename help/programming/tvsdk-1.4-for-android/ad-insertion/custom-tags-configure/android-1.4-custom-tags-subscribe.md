---
description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-title: Assinar tags personalizadas
title: Assinar tags personalizadas
uuid: fe8ba34d-66fc-43bb-b98e-659c1702d1e0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Assinar tags personalizadas{#subscribe-to-custom-tags}

O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.

Antes do início da reprodução, você deve assinar as tags.
Para ser notificado sobre tags personalizadas em manifestos HLS:

Defina os nomes personalizados das tags de publicidade globalmente, transmitindo uma matriz que contenha as tags personalizadas para `setSubscribedTags` o `MediaPlayerItemConfig`.

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

