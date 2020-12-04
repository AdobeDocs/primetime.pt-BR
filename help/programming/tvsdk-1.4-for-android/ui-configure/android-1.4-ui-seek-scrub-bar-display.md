---
description: O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, tanto no vídeo sob demanda (VOD) quanto nos fluxos ao vivo.
seo-description: O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, tanto no vídeo sob demanda (VOD) quanto nos fluxos ao vivo.
seo-title: Exibir uma barra de depuração de busca com a posição de reprodução atual
title: Exibir uma barra de depuração de busca com a posição de reprodução atual
uuid: a9f4dd6c-78cf-455c-8c31-b2f7b740d84a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Exibir uma barra de depuração de busca com a posição de reprodução atual {#display-a-seek-scrub-bar-with-the-current-playback-position}

O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, tanto no vídeo sob demanda (VOD) quanto nos fluxos ao vivo.

>[!IMPORTANT]
>
>A busca em um fluxo ao vivo é permitida apenas para DVR.

1. Configure retornos de chamada para busca.

       A busca é assíncrona, portanto, o TVSDK despacha os seguintes eventos relacionados à busca:
   
   * `QOSEventListener.onSeekStart` - Procure iniciar.
   * `QOSEventListener.onSeekComplete` - Busca bem-sucedida.
   * `QOSEventListener.onOperationFailed` - Falha na busca.

1. Aguarde o player estar em um estado válido para busca.

   Os estados válidos são PREPARADO, COMPLETO, PAUSADO e REPRODUZIDO.

1. Use a SeekBar nativa para definir `OnSeekBarChangeListener` para ver quando o usuário está depurando.
1. Escute `QOSEventListener.onOperationFailed` e tome as ações apropriadas.

   Este evento passa o aviso apropriado. Seu aplicativo determina como continuar, por exemplo, tentando a busca novamente ou a reprodução continuada da posição anterior.

1. Aguarde o TVSDK chamar o retorno de chamada `QOSEventListener.onSeekComplete`.
1. Recupere a posição final ajustada de reprodução usando o parâmetro de posição do retorno de chamada.

   Isso é importante porque a posição real do start após a busca pode ser diferente da posição solicitada. O comportamento de reprodução pode ser afetado se uma busca ou outro reposicionamento terminar no meio de uma pausa de anúncio ou ignorar quebras de anúncio.

1. Use as informações de posição ao exibir uma barra de depuração de busca.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Buscando exemplo**

Neste exemplo, o usuário depura a barra de busca para buscar a posição desejada.

```java
// Use the native SeekBar to set OnSeekBarChangeListener to  
//see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) {  
            // Update the seek bar thumb, with the position provided by the user. 
            setPosition(progress); 
        } 
    } 
 
    @Override 
    public void onStartTrackingTouch(SeekBar seekBar) { 
        isSeeking = true; 
    } 
 
    @Override 
    public void onStopTrackingTouch(SeekBar seekBar) { 
        isSeeking = false; 
        // Retrieve the playback range. 
        TimeRange playbackRange = mediaPlayer.getPlaybackRange(); 
        // Make sure to seek inside the playback range. 
        long seekPosition = Math.min(Math.round(seekBar.getProgress()),  
                                     playbackRange.getDuration()); 
        // Perform seek. 
        seek(playbackRange.getBegin() + seekPosition); 
    } 
}; 
```

