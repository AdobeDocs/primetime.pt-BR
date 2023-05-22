---
description: O TVSDK oferece suporte à busca em uma posição específica (tempo) em que o fluxo seja uma lista de reprodução de janela deslizante, em vídeos sob demanda (VOD) e fluxos ao vivo.
title: Exibir uma barra de limpeza de busca com a posição de reprodução atual
exl-id: d5bc3a54-7dfd-435e-abb4-323639732e0a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Exibir uma barra de limpeza de busca com a posição de reprodução atual {#display-a-seek-scrub-bar-with-the-current-playback-position}

O TVSDK oferece suporte à busca em uma posição específica (tempo) em que o fluxo seja uma lista de reprodução de janela deslizante, em vídeos sob demanda (VOD) e fluxos ao vivo.

>[!TIP]
>
>A busca em um stream ao vivo é permitida somente para DVR.

1. Configure retornos de chamada para busca.

   A busca é assíncrona, portanto, o TVSDK despacha os seguintes eventos relacionados à busca:

   * `MediaPlayerEvent.SEEK_BEGIN`, em que a busca começa.
   * `MediaPlayerEvent.SEEK_END`, em que a busca foi bem-sucedida.
   * `MediaPlayerEvent.OPERATION_FAILED`, em que a busca falhou.

1. Aguarde até que o reprodutor esteja em um status válido para busca.

   Os status válidos são PREPARED, COMPLETE, PAUSED e PLAYING.
1. Usar o nativo `SeekBar` para definir `OnSeekBarChangeListener`, que determina quando o usuário está depurando.
1. Transmita a posição de busca solicitada (milissegundos) para a `MediaPlayer.seek` método.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Você pode buscar somente na duração pesquisável do ativo. Para vídeo sob demanda, isso é do 0 até a duração do ativo.

   >[!TIP]
   >
   >Essa etapa move o indicador de reprodução para uma nova posição no fluxo, mas a posição calculada final pode diferir da posição de busca especificada.

1. Ouvir `MediaPlayerEvent.OPERATION_FAILED` e tomar as medidas adequadas.

   Esse evento passa o aviso apropriado. Seu aplicativo determina como proceder, e as opções incluem tentar a busca novamente ou continuar a reprodução a partir da posição anterior.

1. Aguarde até que o TVSDK chame o `MediaPlayerEvent.SEEK_END` retorno de chamada.
1. Recupere a posição de reprodução ajustada final usando o parâmetro de posição do retorno de chamada.

   Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. As regras, incluindo o comportamento de reprodução, são afetadas se uma busca ou outro reposicionamento terminar no meio de um ad break ou pular ad breaks, puderem ser aplicados.

1. Use as informações de posição ao exibir uma barra de limpeza de busca.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Exemplo de busca**

Neste exemplo, o usuário movimenta a barra de busca para buscar na posição desejada.

```java
//Use the native SeekBar to set an OnSeekBarChangeListener to 
// see when the user is scrubbing. 
seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() { 
    @Override 
    public void onProgressChanged(SeekBar seekBar, int progress, boolean isFromUser) { 
        if (isFromUser) { 
            // Update the seek bar thumb with the position provided by the user. 
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
