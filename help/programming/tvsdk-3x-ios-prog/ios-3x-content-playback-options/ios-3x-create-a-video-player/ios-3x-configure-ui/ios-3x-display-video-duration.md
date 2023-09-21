---
description: Você pode exibir a duração do conteúdo ativo no momento.
title: Exibir a duração do vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Exibir a duração do vídeo {#display-the-duration-of-the-video}

Você pode exibir a duração do conteúdo ativo no momento.

Implemente uma exibição com duração de vídeo usando o seguinte código de amostra:

A variável `PTMediaPlayer` propriedade, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contém o intervalo de janelas pesquisável atual:

* Para VOD, esse intervalo é o intervalo completo de conteúdo de VOD, incluindo anúncios.
* Para live/linear, esse intervalo representa a janela pesquisável.

Para obter mais informações sobre a API, consulte [Referência da API do TVSDK 3.4 para iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
