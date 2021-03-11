---
description: É possível implementar uma barra de controle com suporte a DVR para VOD e transmissão ao vivo. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
title: Construa uma barra de controle aprimorada para DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Construa uma barra de controle aprimorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

É possível implementar uma barra de controle com suporte a DVR para VOD e transmissão ao vivo. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.

* Para VOD, o comprimento da janela que pode ser buscada é a duração do ativo inteiro.
* Para transmissão ao vivo, o comprimento da janela DVR (pesquisável) é definido como o intervalo de tempo que começa na janela de reprodução ao vivo e termina no ponto ativo do cliente.

   O ponto ativo do cliente é calculado subtraindo o comprimento do buffer do final da janela ativa. A duração do target é um valor maior ou igual à duração máxima de um fragmento no manifesto.

   O valor padrão é 10000 ms.

   A barra de controle da reprodução ao vivo oferece suporte a DVR, posicionando primeiro o polegar no ponto de entrada do cliente ao iniciar a reprodução e exibindo uma região que marca a área onde a busca não é permitida.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. Para implementar uma barra de controle com suporte DVR, siga as etapas para exibir uma barra de movimentação, com algumas pequenas diferenças:

   * É possível optar por implementar uma barra de controle mapeada somente para o intervalo pesquisável, em vez de para o intervalo de reprodução. Qualquer interação do usuário para busca pode ser considerada segura no intervalo pesquisável.
   * É possível optar por implementar uma barra de controle que é mapeada para o intervalo de reprodução, mas que também exibe o intervalo pesquisável.

      Para uma barra de controle:
   1. Adicione uma sobreposição à barra de controle que representa o intervalo de reprodução.
   1. Quando o usuário começar a procurar, verifique se a posição de busca desejada está dentro do intervalo pesquisável usando a propriedade `MediaPlayer.seekableRange` .

      Por exemplo:

      ```
      var desiredPosition:Number = // TODO : choose a value 
      
      private function onStatusChange(event:MediaPlayerStatusChangeEvent):void { 
          switch(event.status) { 
              case MediaPlayerStatus.PREPARED: 
                  _mediaPlayer.prepareToPlay(desiredPosition); 
          } 
      }
      ```

      Você também pode optar por buscar o ponto ativo do cliente usando a constante `MediaPlayer.LIVE_POINT`.

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```


