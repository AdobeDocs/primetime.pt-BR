---
description: Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.
title: Exibir a duração, a hora atual e o tempo restante do vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Exibir a duração, a hora atual e o tempo restante do vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.

1. Aguarde o reprodutor estar no estado PREPARADO.
1. Recupere o tempo do indicador de reprodução atual usando o `MediaPlayer.getCurrentTime` método.

   Isso retorna a posição atual do indicador de reprodução na linha do tempo virtual em milissegundos. O tempo é calculado de acordo com o fluxo resolvido que pode conter várias instâncias de conteúdo alternativo, como vários anúncios ou ad breaks fatiados no fluxo principal. Para fluxos ao vivo/lineares, o tempo retornado está sempre no intervalo da janela de reprodução.

   ```java
   long getCurrentTime() throws IllegalStateException;
   ```

1. Recupere o intervalo de reprodução do fluxo e determine a duração.
   1. Use o `mediaPlayer.getPlaybackRange` para obter o intervalo de tempo da linha de tempo virtual.

      ```java
      TimeRange getPlaybackRange() throws IllegalStateException;
      ```

   1. Analisar o intervalo de tempo usando `mediacore.utils.TimeRange`.
   1. Para determinar a duração, subtraia o início do final do intervalo.

      Isso inclui a duração do conteúdo adicional inserido no fluxo (anúncios).

      Para VOD, o intervalo sempre começa com zero e o valor final é igual à soma da duração do conteúdo principal e das durações do conteúdo adicional inserido no fluxo (anúncios).

      Para um ativo linear/em tempo real, o intervalo representa o intervalo da janela de reprodução, que muda durante a reprodução.

      O TVSDK chama o `onUpdated` retorno de chamada para indicar que o item de mídia foi atualizado e que seus atributos (incluindo o intervalo de reprodução) foram atualizados.

1. Use os métodos disponíveis no `MediaPlayer` e a variável `SeekBar` classe que está disponível publicamente no SDK do Android para configurar os parâmetros da barra de busca.

   Por exemplo, este é um layout possível que contém a variável `SeekBar` e dois `TextView` elementos.

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

1. Use um cronômetro para recuperar periodicamente a hora atual e atualizar a SeekBar.

   O exemplo a seguir usa o `Clock.java` classe auxiliar como o temporizador, que está disponível no reprodutor de referência PrimetimeReference. Essa classe define um ouvinte de eventos e aciona um `onTick` evento a cada segundo ou outro valor de tempo limite que você pode especificar.

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

   Em cada tique-taque do relógio, este exemplo recupera a posição atual do reprodutor de mídia e atualiza a SeekBar. Ele usa os dois elementos TextView para marcar a hora atual e a posição final do intervalo de reprodução como valores numéricos.

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
