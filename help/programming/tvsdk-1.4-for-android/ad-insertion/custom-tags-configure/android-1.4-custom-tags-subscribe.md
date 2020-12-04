---
description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-title: Assinar tags personalizadas
title: Assinar tags personalizadas
uuid: fe8ba34d-66fc-43bb-b98e-659c1702d1e0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

---


# Inscrever-se em tags personalizadas{#subscribe-to-custom-tags}

O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.

Antes dos start de reprodução, você deve assinar as tags.
Para ser notificado sobre tags personalizadas em manifestos HLS:

Defina os nomes de tags de publicidade personalizadas globalmente transmitindo uma matriz que contenha as tags personalizadas para `setSubscribedTags` em `MediaPlayerItemConfig`.

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

