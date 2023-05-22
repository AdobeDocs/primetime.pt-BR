---
description: Você pode implementar uma barra de controle com suporte a DVR para VOD e transmissão ao vivo. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
title: Construir uma barra de controle aprimorada para DVR
exl-id: a812f2d5-f1ee-4df6-9cc7-e39f55ec26f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Construir uma barra de controle aprimorada para DVR{#construct-a-control-bar-enhanced-for-dvr}

Você pode implementar uma barra de controle com suporte a DVR para VOD e transmissão ao vivo. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.

* Para VOD, o comprimento da janela pesquisável é a duração do ativo inteiro.
* Para transmissão ao vivo, o comprimento da janela DVR (pesquisável) é definido como o intervalo de tempo que começa na janela de reprodução ao vivo e termina no ponto de vida do cliente.

   O ponto ativo do cliente é calculado subtraindo o comprimento do buffer do final da janela ativa. A duração alvo é um valor maior ou igual à duração máxima de um fragmento no manifesto.

   O valor padrão é 10000 ms.

   A barra de controle para reprodução ao vivo suporta DVR, posicionando primeiro o polegar no ponto ao vivo do cliente ao iniciar a reprodução e exibindo uma região que marca a área onde a busca não é permitida.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. Para implementar uma barra de controle com suporte a DVR, siga as etapas para exibir uma barra de limpeza de busca, com algumas pequenas diferenças:

   * Você pode optar por implementar uma barra de controle mapeada somente para o intervalo pesquisável, em vez de para o intervalo de reprodução. Qualquer interação do usuário para busca pode ser considerada segura no intervalo pesquisável.
   * Você pode optar por implementar uma barra de controle que esteja mapeada para o intervalo de reprodução, mas que também exiba o intervalo pesquisável.

      Para uma barra de controle:
   1. Adicione uma sobreposição à barra de controle que representa o intervalo de reprodução.
   1. Quando o usuário começar a busca, verifique se a posição de busca desejada está dentro do intervalo pesquisável usando `MediaPlayer.getSeekableRange`.

      Por exemplo:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      Você também pode optar por buscar para o ponto de acesso do cliente usando o `MediaPlayer.LIVE_POINT` constante.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
