---
description: O TVSDK permite a busca em uma posição específica (tempo) em que o fluxo é uma lista de reprodução de janela deslizante, em fluxos de vídeo sob demanda (VOD) e ao vivo.
title: Exibir uma barra de limpeza de busca com a posição de reprodução atual
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Exibir uma barra de limpeza de busca com a posição de reprodução atual {#display-a-seek-scrub-bar-with-the-current-playback-position}

O TVSDK permite a busca em uma posição específica (tempo) em que o fluxo é uma lista de reprodução de janela deslizante, em fluxos de vídeo sob demanda (VOD) e ao vivo.

>[!IMPORTANT]
>
>A busca em um stream ao vivo é permitida somente para DVR.

1. Configure retornos de chamada para busca.

       A busca é assíncrona, portanto, o TVSDK despacha os seguintes eventos relacionados à busca:
   
   * `QOSEventListener.onSeekStart` - Início da busca.
   * `QOSEventListener.onSeekComplete` - Busca bem-sucedida.
   * `QOSEventListener.onOperationFailed` - Falha na busca.

1. Aguarde até que o reprodutor esteja em um estado válido para busca.

   Os estados válidos são PREPARED, COMPLETE, PAUSED e PLAYING.

1. Use a SeekBar nativa para definir `OnSeekBarChangeListener` para ver quando o usuário está depurando.
1. Ouvir `QOSEventListener.onOperationFailed` e tomar as medidas adequadas.

   Esse evento passa o aviso apropriado. O aplicativo determina como proceder, por exemplo, tentando a busca novamente ou continuando a reprodução a partir da posição anterior.

1. Aguarde até que o TVSDK chame o `QOSEventListener.onSeekComplete` retorno de chamada.
1. Recupere a posição de reprodução ajustada final usando o parâmetro de posição do retorno de chamada.

   Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. O comportamento da reprodução pode ser afetado se uma busca ou outro reposicionamento terminar no meio de um ad break ou pular ad breaks.

1. Use as informações de posição ao exibir uma barra de limpeza de busca.

<!--<a id="example_9657AA855B6A4355B0E7D854596FFB54"></a>-->

**Exemplo de busca**

Neste exemplo, o usuário movimenta a barra de busca para buscar na posição desejada.

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
