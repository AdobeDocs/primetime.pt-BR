---
description: Você pode exibir a duração do conteúdo ativo no momento.
title: Exibir a duração do vídeo
exl-id: 4e31d784-4d16-470b-8317-11be32a55c2f
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Exibir a duração do vídeo {#display-the-duration-of-the-video}

Você pode exibir a duração do conteúdo ativo no momento.

Implemente uma exibição com duração de vídeo usando o seguinte código de amostra:

A variável `PTMediaPlayer` propriedade, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contém o intervalo de janelas pesquisável atual:

* Para VOD, esse intervalo é o intervalo completo de conteúdo de VOD, incluindo anúncios.
* Para live/linear, esse intervalo representa a janela pesquisável.

Para obter mais informações sobre a API, consulte [Referência da API do TVSDK 1.4 para iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
