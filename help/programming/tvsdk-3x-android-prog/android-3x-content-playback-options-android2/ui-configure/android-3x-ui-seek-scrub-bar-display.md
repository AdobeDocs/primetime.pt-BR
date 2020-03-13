---
description: O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, em vídeo sob demanda (VOD) e fluxos ao vivo.
seo-description: O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, em vídeo sob demanda (VOD) e fluxos ao vivo.
seo-title: Exibir uma barra de depuração de busca com a posição de reprodução atual
title: Exibir uma barra de depuração de busca com a posição de reprodução atual
uuid: 30a9237c-bbd5-457e-a93c-662570711986
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Exibir uma barra de depuração de busca com a posição de reprodução atual {#display-a-seek-scrub-bar-with-the-current-playback-position}

O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, em vídeo sob demanda (VOD) e fluxos ao vivo.

>[!TIP]
>
>A busca em um fluxo ao vivo é permitida apenas para DVR.

1. Configure retornos de chamada para busca.

   A busca é assíncrona, portanto, o TVSDK despacha os seguintes eventos relacionados à busca:

   * `MediaPlayerEvent.SEEK_BEGIN`, onde a busca começa.
   * `MediaPlayerEvent.SEEK_END`, quando a procura for bem sucedida.
   * `MediaPlayerEvent.OPERATION_FAILED`, onde a busca falhou.

1. Aguarde o player ter um status válido para busca.

   Os status válidos são PREPARADO, COMPLETO, PAUSADO e REPRODUZIDO.
1. Use nativo `SeekBar` para definir `OnSeekBarChangeListener`, que determina quando o usuário está depurando.
1. Passe a posição de busca solicitada (milissegundos) para o `MediaPlayer.seek` método.

   ```java
   void seek(long position) throws MediaPlayerException;
   ```

   Você pode procurar apenas na duração pesquisável do ativo. Para vídeo sob demanda, que é de 0 até a duração do ativo.

   >[!TIP]
   >
   >Essa etapa move o indicador de reprodução para uma nova posição no fluxo, mas a posição final calculada pode diferir da posição de busca especificada.

1. Escute `MediaPlayerEvent.OPERATION_FAILED` e tome as medidas apropriadas.

   Esse evento passa pelo aviso apropriado. Seu aplicativo determina como prosseguir e as opções incluem tentar a busca novamente ou continuar a reprodução a partir da posição anterior.

1. Aguarde o TVSDK ligar para o `MediaPlayerEvent.SEEK_END` retorno de chamada.
1. Recupere a posição final ajustada de reprodução usando o parâmetro de posição do retorno de chamada.

   Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. As regras, incluindo o comportamento de reprodução, serão afetadas se uma busca ou outro reposicionamento terminar no meio de uma pausa de anúncio ou se ignorar pausas de anúncio, poderão ser aplicadas.

1. Use as informações de posição ao exibir uma barra de depuração de busca.

<!--<a id="example_EEB73818260C43C8B5AE12BA68548AB7"></a>-->

**Buscando exemplo**

Neste exemplo, o usuário depura a barra de busca para buscar a posição desejada.

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
