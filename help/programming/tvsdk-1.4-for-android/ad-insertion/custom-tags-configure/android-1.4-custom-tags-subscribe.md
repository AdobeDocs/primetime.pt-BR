---
description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.
title: Inscrever-se em tags personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Inscrever-se em tags personalizadas{#subscribe-to-custom-tags}

O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.

Antes de começar a reprodução, você deve assinar as tags.
Para ser notificado sobre tags personalizadas em manifestos HLS:

Defina os nomes das tags de anúncio personalizadas globalmente, transmitindo uma matriz que contém as tags personalizadas para `setSubscribedTags` in `MediaPlayerItemConfig`.

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
