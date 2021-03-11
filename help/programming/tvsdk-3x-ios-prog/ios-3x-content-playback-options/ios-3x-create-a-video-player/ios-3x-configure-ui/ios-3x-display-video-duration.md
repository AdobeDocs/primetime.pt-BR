---
description: Você pode exibir a duração do conteúdo ativo no momento.
title: Exibir a duração do vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# Exibir a duração do vídeo {#display-the-duration-of-the-video}

Você pode exibir a duração do conteúdo ativo no momento.

Implemente uma exibição de duração do vídeo usando o seguinte código de amostra:

    A propriedade `PTMediaPlayer`, ` [SekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)`, contém o intervalo de janelas buscável atual:
    
    * Para VOD, esse intervalo é todo o intervalo de conteúdo de VOD, incluindo anúncios.
    * Para live/linear, esse intervalo representa a janela pesquisável.
    
    Para obter mais informações sobre a API, consulte [TVSDK 3.4 para referência à API do iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
