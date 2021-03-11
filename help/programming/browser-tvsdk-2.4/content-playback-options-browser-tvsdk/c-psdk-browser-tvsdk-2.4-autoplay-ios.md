---
title: Reprodução automática no iOS
description: Reprodução automática no iOS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---


# Reprodução automática no iOS{#autoplay-on-ios}

A implementação da API de volume do AdobePSDK.MediaPlayer permite a reprodução automática de conteúdo em dispositivos que executam o iOS versão 10 ou superior. O iOS permite a reprodução automática somente quando o volume está sem áudio. Quando o volume é definido como zero, a API define a propriedade `muted` da tag de vídeo como `true`, caso contrário, a propriedade `muted` é definida como `false`. A API `play` inicia a reprodução sem nenhuma interação do usuário ou gesto do usuário.

Para reprodução automática no iPhone, defina também a propriedade `playsInline` da tag `video` para `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>O uso da propriedade `playsInline` inicia a reprodução sem o modo de tela cheia.

