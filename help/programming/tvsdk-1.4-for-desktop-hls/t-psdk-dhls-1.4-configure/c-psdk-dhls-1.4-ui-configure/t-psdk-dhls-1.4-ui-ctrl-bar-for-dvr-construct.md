---
description: Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
seo-description: Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
seo-title: Construa uma barra de controle aprimorada para DVR
title: Construa uma barra de controle aprimorada para DVR
uuid: 08f943e8-90da-4860-92dd-dd289fd68cba
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Construa uma barra de controle aprimorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.

* Para VOD, o comprimento da janela pesquisável é a duração do ativo inteiro.
* Para transmissão ao vivo, o comprimento da janela DVR (pesquisável) é definido como o intervalo de tempo que começa na janela de reprodução ao vivo e termina no ponto ativo do cliente.

   O ponto ativo do cliente é calculado subtraindo o comprimento do buffer do final da janela ativa. A duração do destino é um valor maior ou igual à duração máxima de um fragmento no manifesto.

   O valor padrão é 10000 ms.

   A barra de controle para reprodução ao vivo suporta DVR ao posicionar primeiro a miniatura no ponto ativo do cliente ao iniciar a reprodução e ao exibir uma região que marca a área na qual a busca não é permitida.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. Para implementar uma barra de controle com suporte a DVR, siga as etapas para exibir uma barra de depuração de busca, com algumas pequenas diferenças:

   * Você pode optar por implementar uma barra de controle que seja mapeada somente para o intervalo pesquisável em vez de para o intervalo de reprodução. Qualquer interação do usuário para busca pode ser considerada segura no intervalo pesquisável.
   * Você pode optar por implementar uma barra de controle que esteja mapeada para o intervalo de reprodução, mas que também exiba o intervalo pesquisável.

      Para uma barra de controle:
   1. Adicione uma sobreposição à barra de controle que representa o intervalo de reprodução.
   1. Quando o usuário começar a buscar, verifique se a posição de busca desejada está dentro do intervalo pesquisável usando a `MediaPlayer.seekableRange` propriedade.

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

      Você também pode optar por buscar o ponto ativo do cliente usando a `MediaPlayer.LIVE_POINT` constante.

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```


