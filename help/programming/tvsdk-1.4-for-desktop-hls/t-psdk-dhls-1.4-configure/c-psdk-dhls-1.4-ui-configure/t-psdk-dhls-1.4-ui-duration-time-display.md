---
description: Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.
title: Exibir a duração, a hora atual e o tempo restante do vídeo
exl-id: 490bfa22-6df6-44a3-8e0d-9bb5939ae881
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Exibir a duração, a hora atual e o tempo restante do vídeo{#display-the-duration-current-time-and-remaining-time-of-the-video}

Você pode usar o TVSDK para recuperar informações sobre a mídia que pode ser exibida na barra de busca.

1. Aguarde até que o reprodutor esteja com o status INICIALIZADO.
1. Recupere o tempo do indicador de reprodução atual usando o `MediaPlayer.currentTime` propriedade.

   Isso retorna a posição atual do indicador de reprodução na linha do tempo virtual em milissegundos. O tempo é calculado de acordo com o fluxo resolvido que pode conter várias instâncias de conteúdo alternativo, como vários anúncios ou ad breaks fatiados no fluxo principal. Para fluxos ao vivo/lineares, o tempo retornado está sempre no intervalo da janela de reprodução.

   ```
   function get currentTime():Number;
   ```

1. Recupere o intervalo de reprodução do fluxo e determine a duração.
   1. Use o `mediaPlayer.playbackRange` para obter o intervalo de tempo da linha de tempo virtual.

      ```
      function get playbackRange():TimeRange;
      ```

   1. Analisar o intervalo de tempo usando `mediacore.utils.TimeRange`.
   1. Para determinar a duração, subtraia o início do final do intervalo.

      Isso inclui a duração do conteúdo adicional inserido no fluxo (anúncios).

      Para VOD, o intervalo sempre começa com zero e o valor final é igual à soma da duração do conteúdo principal e das durações do conteúdo adicional inserido no fluxo (anúncios).

      Para um ativo linear/em tempo real, o intervalo representa o intervalo da janela de reprodução, que muda durante a reprodução.

      O TVSDK despacha um `MediaPlayerItemEvent.ITEM_UPDATED` evento para indicar que o item de mídia foi atualizado e que seus atributos (incluindo o intervalo de reprodução) foram atualizados.

1. Use os métodos disponíveis no `MediaPlayer` e a variável `HSlider` classe que está disponível publicamente no SDK do Flex para configurar os parâmetros da barra de busca.

1. Use um cronômetro para recuperar periodicamente a hora atual e atualizar a `SeekBar`.
