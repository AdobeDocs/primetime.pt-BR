---
description: Você pode usar o TVSDK para recuperar informações sobre a posição do reprodutor na mídia e exibi-lo na barra de busca.
title: Exibir a duração, o tempo atual e o tempo restante do vídeo
exl-id: 68501c81-346a-4c3e-aa20-a98b8b1c6b17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# Exibir a duração, o tempo atual e o tempo restante do vídeo {#display-the-duration-current-time-and-remaining-time-of-the-video}

Você pode usar o TVSDK para recuperar informações sobre a posição do reprodutor na mídia e exibi-lo na barra de busca.

1. Aguarde até que o reprodutor esteja pelo menos no estado PREPARADO.
1. Recupere o tempo atual do indicador de reprodução usando o `MediaPlayer.getCurrentTime` método .

   Isso retorna a posição atual do indicador de reprodução na linha do tempo virtual, em milissegundos. O tempo é calculado em relação ao fluxo resolvido, que pode conter várias instâncias de conteúdo alternativo, como vários anúncios ou quebras de anúncios segmentados no fluxo principal. Para fluxos ao vivo/lineares, o tempo retornado está sempre no intervalo da janela de reprodução.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. Recupere o intervalo de reprodução do fluxo e determine a duração.
   1. Use o `MediaPlayer.getPlaybackRange` para obter o intervalo de tempo da linha do tempo virtual.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. Use o `MediaPlayer.getPlaybackRange` para obter o intervalo de tempo da linha do tempo virtual.

      * Para VOD, o intervalo sempre começa com zero e o valor final é igual à soma da duração do conteúdo principal e das durações do conteúdo adicional no fluxo (anúncios).
      * Para um ativo linear/ao vivo, o intervalo representa o intervalo da janela de reprodução. Esse intervalo muda durante a reprodução.

         O TVSDK chama a função `ITEM_Updated` retorno de chamada para indicar que o item de mídia foi atualizado e que seus atributos, incluindo o intervalo de reprodução, foram atualizados.

1. Use os métodos disponíveis em `MediaPlayer` e no `SeekBar` no Android SDK para configurar os parâmetros da barra de busca.

   Por exemplo, aqui está um layout possível que contém a barra de busca e dois `TextView` elementos.

   ```xml
   <LinearLayout 
    android:id="@+id/controlBarLayout" 
    android:layout_width="match_parent" 
    android:layout_height="wrap_content" 
    android:layout_alignParentBottom="true" 
    android:background="@android:color/black" 
    android:orientation="horizontal" > 
    <TextView 
       android:id="@+id/playerCurrentTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
    <SeekBar 
       android:id="@+id/playerSeekBar" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_weight="1" /> 
    <TextView 
       android:id="@+id/playerTotalTimeText" 
       android:layout_width="wrap_content" 
       android:layout_height="wrap_content" 
       android:layout_margin="7dp" 
       android:text="00:00" 
       android:textColor="@android:color/white" /> 
   </LinearLayout>
   ```

1. Use um temporizador para recuperar periodicamente a hora atual e atualizar a barra de busca, conforme mostrado na figura:

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width="477.000pt"}

   O exemplo a seguir usa a variável `Clock.java` classe helper, que está disponível em `ReferencePlayer`, como o temporizador. Essa classe define um ouvinte de evento e aciona um `onTick` a cada segundo ou outro valor de tempo limite que pode ser especificado.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           // Timer event is received. Update the seek bar here. 
       } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   Em cada marca de relógio, esse exemplo recupera a posição atual do reprodutor de mídia e atualiza a barra de busca. Usa os dois `TextView` elementos para marcar a hora atual e a posição final do intervalo de reprodução como valores numéricos.

   ```java
   @Override 
   public void onTick(String name) { 
       if (mediaPlayer != null &&  
         mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
           handler.post(new Runnable() { 
               @Override 
               public void run() { 
                   seekBar.setProgress((int) mediaPlayer.getCurrentTime()); 
                   currentTimeText.setText(timeStampToText(mediaPlayer.getCurrentTime())); 
                   totalTimeText.setText(timeStampToText(mediaPlayer.getPlaybackRange().getEnd())); 
               } 
           }); 
       } 
   } 
   ```
