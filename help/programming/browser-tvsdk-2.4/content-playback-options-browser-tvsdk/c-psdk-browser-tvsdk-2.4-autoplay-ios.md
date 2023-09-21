---
title: Reprodução automática no iOS
description: Reprodução automática no iOS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# Reprodução automática no iOS{#autoplay-on-ios}

A implementação da API de volume do AdobePSDK.MediaPlayer permite a reprodução automática de conteúdo em dispositivos que executam o iOS versão 10 ou superior. O iOS permite a reprodução automática somente quando o volume está sem áudio. Quando o volume é definido como zero, a API define o `muted` propriedade da tag de vídeo para `true`, caso contrário, o `muted` propriedade está definida como `false`. A variável `play` A API inicia a reprodução sem nenhuma interação ou gesto do usuário.

Para reprodução automática no iPhone, defina também a variável `playsInline` propriedade do `video` para `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>Uso do `playsInline` A propriedade inicia a reprodução sem o modo de tela cheia.
