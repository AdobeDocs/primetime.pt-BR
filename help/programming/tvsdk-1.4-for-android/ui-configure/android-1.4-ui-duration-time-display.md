---
description: Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.
seo-description: Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.
seo-title: Exibir a duração, o tempo atual e o tempo restante do vídeo
title: Exibir a duração, o tempo atual e o tempo restante do vídeo
uuid: afb43169-2d82-4137-ba38-27caef3d8c21
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Exibir a duração, o tempo atual e o tempo restante do vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.

1. Aguarde o player estar no estado PREPARADO.
1. Recupere a hora atual do indicador de reprodução usando o método `MediaPlayer.getCurrentTime`.

   Isso retorna a posição atual do indicador de reprodução na linha do tempo virtual em milissegundos. O tempo é calculado em relação ao fluxo resolvido, que pode conter várias instâncias de conteúdo alternativo, como várias publicidades ou quebras de anúncio divididas no fluxo principal. Para fluxos ao vivo/lineares, o tempo retornado está sempre no intervalo da janela de reprodução.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Recupere o intervalo de reprodução do fluxo e determine a duração.
   1. Use o método `mediaPlayer.getPlaybackRange` para obter o intervalo de tempo da linha do tempo virtual.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Analise o intervalo de tempo usando `mediacore.utils.TimeRange`.
   1. Para determinar a duração, subtraia o start do final do intervalo.

      Isso inclui a duração do conteúdo adicional inserido no fluxo (anúncios).

      Para VOD, o intervalo sempre começa com zero e o valor final é igual à soma da duração do conteúdo principal e da duração do conteúdo adicional inserido no fluxo (anúncios).

      Para um ativo linear/ativo, o intervalo representa o intervalo da janela de reprodução e esse intervalo muda durante a reprodução.

      O TVSDK chama seu retorno de chamada `onUpdated` para indicar que o item de mídia foi atualizado e que seus atributos (incluindo o intervalo de reprodução) foram atualizados.

1. Use os métodos disponíveis nas classes `MediaPlayer` e `SeekBar` que estão publicamente disponíveis no Android SDK para configurar os parâmetros da barra de busca.

   Por exemplo, este é um possível layout que contém os elementos `SeekBar` e `TextView`.

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

1. Use um temporizador para recuperar periodicamente a hora atual e atualizar a SeekBar.

   O exemplo a seguir usa a classe auxiliar `Clock.java` como timer, que está disponível no player de referência PrimetimeReference. Essa classe define um ouvinte de evento e aciona um evento `onTick` a cada segundo, ou outro valor de tempo limite que você pode especificar.

   ```java
   playbackClock = new Clock(PLAYBACK_CLOCK, CLOCK_TIMER); 
   playbackClockEventListener = new Clock.ClockEventListener() { 
   @Override 
   public void onTick(String name) { 
       // Timer event is received. Update the SeekBar here. 
   } 
   }; 
   playbackClock.addClockEventListener(playbackClockEventListener);
   ```

   Em cada marca de relógio, este exemplo recupera a posição atual do player de mídia e atualiza a SeekBar. Ele usa os dois elementos TextView para marcar a hora atual e a posição final do intervalo de reprodução como valores numéricos.

   ```java
   @Override 
   public void onTick(String name) { 
   if (mediaPlayer != null && mediaPlayer.getStatus() == PlayerState.PLAYING) { 
       handler.post(new Runnable() { 
           @Override 
           public void run() { 
               seekBar.setProgress((int)  
                    mediaPlayer.getCurrentTime()); 
               currentTimeText.setText(timeStampToText( 
                  mediaPlayer.getCurrentTime())); 
               totalTimeText.setText(timeStampToText( 
                   mediaPlayer.getPlaybackRange().getEnd())); 
           } 
       }); 
   } 
   }
   ```

