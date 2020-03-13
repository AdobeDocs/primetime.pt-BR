---
description: nulo
seo-description: nulo
seo-title: Reprodução automática no iOS
title: Reprodução automática no iOS
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Reprodução automática no iOS{#autoplay-on-ios}

A implementação da API de volume do AdobePSDK.MediaPlayer permite a reprodução automática de conteúdo em dispositivos que executam o iOS versão 10 ou superior. O iOS permite a reprodução automática somente quando o volume está silenciado. Quando o volume é definido como zero, a API define a `muted` propriedade da tag de vídeo como `true`, caso contrário, a `muted` propriedade é definida como `false`. A `play` API inicia a reprodução sem nenhuma interação do usuário ou gesto do usuário.

Para reprodução automática no iPhone, defina adicionalmente a propriedade `playsInline` da `video` tag como `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>O uso da `playsInline` propriedade inicia a reprodução sem o modo de tela cheia.

