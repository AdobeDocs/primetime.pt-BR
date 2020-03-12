---
description: Você pode exibir a duração do conteúdo ativo no momento.
seo-description: Você pode exibir a duração do conteúdo ativo no momento.
seo-title: Exibir a duração do vídeo
title: Exibir a duração do vídeo
uuid: 945f222d-80ba-4832-a06f-9bb8db6adbcb
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Exibir a duração do vídeo {#display-the-duration-of-the-video}

Você pode exibir a duração do conteúdo ativo no momento.

Implemente uma exibição de duração do vídeo usando o seguinte código de amostra:

    A propriedade `PTMediaPlayer&#39;, &#39; [buskableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)&#39;, contém o intervalo de janelas pesquisáveis atual:
    
    * Para VOD, esse intervalo é todo o intervalo de conteúdo VOD, incluindo anúncios.
    * Para live/linear, esse intervalo representa a janela que pode ser buscada.
    
    Para obter mais informações sobre a API, consulte [TVSDK 3.4 para referência à API do iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
