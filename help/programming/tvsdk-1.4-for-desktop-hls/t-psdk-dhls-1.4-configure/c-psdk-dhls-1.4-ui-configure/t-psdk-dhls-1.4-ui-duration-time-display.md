---
description: Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.
title: Exibir a duração, o tempo atual e o tempo restante do vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Exibir a duração, o tempo atual e o tempo restante do vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.

1. Aguarde até que o reprodutor esteja no status INITIALIZED .
1. Recupere o tempo atual do indicador de reprodução usando a propriedade `MediaPlayer.currentTime`.

   Isso retorna a posição atual do indicador de reprodução na linha do tempo virtual, em milissegundos. O tempo é calculado em relação ao fluxo resolvido, que pode conter várias instâncias de conteúdo alternativo, como vários anúncios ou quebras de anúncios segmentados no fluxo principal. Para fluxos ao vivo/lineares, o tempo retornado está sempre no intervalo da janela de reprodução.

   ```
   function get currentTime():Number;
   ```

1. Recupere o intervalo de reprodução do fluxo e determine a duração.
   1. Use a propriedade `mediaPlayer.playbackRange` para obter o intervalo de tempo da linha do tempo virtual.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Analise o intervalo de tempo usando `mediacore.utils.TimeRange`.
   1. Para determinar a duração, subtraia o início do final do intervalo.

      Isso inclui a duração do conteúdo adicional inserido no fluxo (anúncios).

      Para VOD, o intervalo sempre começa com zero e o valor final é igual à soma da duração do conteúdo principal e das durações do conteúdo adicional inserido no fluxo (anúncios).

      Para um ativo linear/ao vivo, o intervalo representa o intervalo da janela de reprodução e esse intervalo muda durante a reprodução.

      O TVSDK despacha um evento `MediaPlayerItemEvent.ITEM_UPDATED` para indicar que o item de mídia foi atualizado e que seus atributos (incluindo o intervalo de reprodução) foram atualizados.

1. Use os métodos disponíveis nas classes `MediaPlayer` e `HSlider` que estão disponíveis publicamente no SDK do Flex para configurar os parâmetros da barra de busca.

1. Use um temporizador para recuperar periodicamente a hora atual e atualizar o `SeekBar`.
