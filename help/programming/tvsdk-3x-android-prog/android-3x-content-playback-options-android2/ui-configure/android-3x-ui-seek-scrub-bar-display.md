---
description: O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, em vídeos sob demanda (VOD) e fluxos ao vivo.
title: Exibir uma barra de movimentação com a posição de reprodução atual
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Exibir uma barra de movimentação com a posição de reprodução atual {#display-a-seek-scrub-bar-with-the-current-playback-position}

O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, em vídeos sob demanda (VOD) e fluxos ao vivo.

>[!TIP]
>
>A busca em direto só é permitida para DVR.

1. Configurar retornos de chamada para busca.

   A busca é assíncrona, portanto, o TVSDK despacha os seguintes eventos relacionados à busca:

   * `MediaPlayerEvent.SEEK_BEGIN`, onde a busca começa.
   * `MediaPlayerEvent.SEEK_END`, em que a busca é bem-sucedida.
   * `MediaPlayerEvent.OPERATION_FAILED`, em que a busca falhou.

1. Aguarde até que o reprodutor esteja em um status válido para busca.

   Os status válidos são PREPARED, COMPLETE, PAUSED e PLAYING.
1. Use o nativo `SeekBar` para definir `OnSeekBarChangeListener`, que determina quando o usuário está depurando.
1. Passe a posição de busca solicitada (milissegundos) para o método `MediaPlayer.seek`.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Você pode procurar somente na duração pesquisável do ativo. Para vídeo sob demanda, ou seja, de 0 à duração do ativo.

   >[!TIP]
   >
   >Essa etapa move o indicador de reprodução para uma nova posição no fluxo, mas a posição final calculada pode ser diferente da posição de busca especificada.

1. Escute `MediaPlayerEvent.OPERATION_FAILED` e execute as ações apropriadas.

   Esse evento passa o aviso apropriado. Seu aplicativo determina como proceder e as opções incluem tentar a busca novamente ou continuar a reprodução na posição anterior.

1. Aguarde TVSDK chamar o retorno de chamada `MediaPlayerEvent.SEEK_END`.
1. Recupere a posição final de reprodução ajustada usando o parâmetro de posição do retorno de chamada.

   Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. As regras, incluindo o comportamento de reprodução, serão afetadas se uma busca ou outro reposicionamento terminar no meio de uma pausa de anúncio ou ignorar quebras de anúncio.

1. Use as informações de posição ao exibir uma barra de movimentação.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Exemplo de busca**

Neste exemplo, o usuário movimenta a barra de busca para buscar a posição desejada.

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
