---
description: Você pode exibir a duração do conteúdo ativo no momento.
seo-description: Você pode exibir a duração do conteúdo ativo no momento.
seo-title: Exibir a duração do vídeo
title: Exibir a duração do vídeo
uuid: 02042070-9c55-4cbb-9dc1-49987451eb8f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Exibir a duração do vídeo {#display-the-duration-of-the-video}

Você pode exibir a duração do conteúdo ativo no momento.

Implemente uma exibição de duração do vídeo usando o seguinte código de amostra:

    A propriedade `PTMediaPlayer&#39;, [SEKableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contém o intervalo de janelas pesquisável atual:
    
    * Para VOD, esse intervalo é o intervalo de conteúdo VOD inteiro, incluindo anúncios.
    * Para live/linear, esse intervalo representa a janela que pode ser buscada.
    
    Para obter mais informações sobre a API, consulte [TVSDK 1.4 para referência à API do iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
