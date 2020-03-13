---
description: Você pode usar o TVSDK para recuperar informações sobre a posição do player na mídia e exibi-las na barra de busca.
seo-description: Você pode usar o TVSDK para recuperar informações sobre a posição do player na mídia e exibi-las na barra de busca.
seo-title: Exibir a duração, o tempo atual e o tempo restante do vídeo
title: Exibir a duração, o tempo atual e o tempo restante do vídeo
uuid: 13627fa2-8cd8-4336-bc4b-7e3226330389
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Exibir a duração, o tempo atual e o tempo restante do vídeo {#display-the-duration-current-time-and-remaining-time-of-the-video}

Você pode usar o TVSDK para recuperar informações sobre a posição do player na mídia e exibi-las na barra de busca.

1. Aguarde até que o player esteja pelo menos no estado PREPARADO.
1. Recupere o tempo atual do indicador de reprodução usando o `MediaPlayer.getCurrentTime` método.

   Isso retorna a posição atual do indicador de reprodução na linha do tempo virtual em milissegundos. O tempo é calculado em relação ao fluxo resolvido, que pode conter várias instâncias de conteúdo alternativo, como várias publicidades ou quebras de anúncio divididas no fluxo principal. Para fluxos ao vivo/lineares, o tempo retornado está sempre no intervalo da janela de reprodução.

   ```java
   long getCurrentTime() throws MediaPlayerException;
   ```

1. Recupere o intervalo de reprodução do fluxo e determine a duração.
   1. Use o `MediaPlayer.getPlaybackRange` método para obter o intervalo de tempo da linha do tempo virtual.

      ```java
      TimeRange getPlaybackRange() throws MediaPlayerException;
      ```

   1. Use o `MediaPlayer.getPlaybackRange` método para obter o intervalo de tempo da linha do tempo virtual.

      * Para VOD, o intervalo sempre começa com zero e o valor final é igual à soma da duração do conteúdo principal e da duração do conteúdo adicional no fluxo (anúncios).
      * Para um ativo linear/ativo, o intervalo representa o intervalo da janela de reprodução. Este intervalo muda durante a reprodução.

         O TVSDK chama o `ITEM_Updated` retorno de chamada para indicar que o item de mídia foi atualizado e que seus atributos, incluindo o intervalo de reprodução, foram atualizados.

1. Use os métodos disponíveis na classe `MediaPlayer` e na `SeekBar` classe no Android SDK para configurar os parâmetros da barra de busca.

   Por exemplo, este é um layout possível que contém a barra de busca e dois `TextView` elementos.

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

1. Use um temporizador para recuperar periodicamente a hora atual e atualizar a barra de busca, como mostrado na figura:

   <!--<a id="fig_689CEDDD02094C0C8E91C5195F8EAD3F"></a>-->

   ![](assets/seek-bar.jpg){width=&quot;477.000pt&quot;}

   O exemplo a seguir usa a classe `Clock.java` helper, que está disponível em `ReferencePlayer`, como o timer. Essa classe define um ouvinte de evento e aciona um `onTick` evento a cada segundo ou outro valor de tempo limite que você pode especificar.

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

   Em cada marca de relógio, esse exemplo recupera a posição atual do player de mídia e atualiza a barra de busca. Ele usa os dois `TextView` elementos para marcar a hora atual e a posição final do intervalo de reprodução como valores numéricos.

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

