---
description: nulo
seo-description: nulo
seo-title: Reprodução automática no iOS
title: Reprodução automática no iOS
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# Reprodução automática no iOS{#autoplay-on-ios}

A implementação da API de volume do AdobePSDK.MediaPlayer permite a reprodução automática de conteúdo em dispositivos que executam o iOS versão 10 ou superior. O iOS permite a reprodução automática somente quando o volume está silenciado. Quando o volume é definido como zero, a API define a propriedade `muted` da tag de vídeo como `true`, caso contrário a propriedade `muted` é definida como `false`. A API `play` start a reprodução sem nenhuma interação do usuário ou gesto do usuário.

Para reprodução automática no iPhone, defina adicionalmente a propriedade `playsInline` da tag `video` como `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>O uso da propriedade `playsInline` start a reprodução sem o modo de tela cheia.

