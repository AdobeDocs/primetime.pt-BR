---
description: Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
seo-description: Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.
seo-title: Construa uma barra de controle aprimorada para DVR
title: Construa uma barra de controle aprimorada para DVR
uuid: 71bfceef-baf0-40ad-a7a0-fa2e22d24e31
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Construa uma barra de controle aprimorada para DVR {#construct-a-control-bar-enhanced-for-dvr}

Você pode implementar uma barra de controle com suporte a DVR para transmissão ao vivo e VOD. O suporte a DVR inclui o conceito de uma janela pesquisável e o ponto ativo do cliente.

* Para VOD, o comprimento da janela pesquisável é a duração do ativo inteiro.
* Para transmissão ao vivo, o comprimento da janela DVR (pesquisável) é definido como o intervalo de tempo que start na janela de reprodução ao vivo e termina no ponto ativo do cliente.

   Lembre-se das seguintes informações:

   * O ponto ativo do cliente é calculado subtraindo o comprimento do buffer do final da janela ativa.

      A duração do público alvo é um valor maior ou igual à duração máxima de um fragmento no manifesto.
   * O valor padrão é 10000 ms.
   * A barra de controle para reprodução ao vivo suporta DVR ao posicionar primeiro a miniatura no ponto ativo do cliente ao iniciar a reprodução e ao exibir uma região que marca a área na qual a busca não é permitida.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. Para implementar uma barra de controle com suporte a DVR, siga as etapas em [Exibir uma barra de depuração de busca com a posição de reprodução atual...](../../../tvsdk-2.7-for-android/content-playback-options/ui-configure/t-psdk-android-2.7-ui-seek-scrub-bar-display.md) com as seguintes diferenças:

   * Você pode implementar uma barra de controle que é mapeada somente para o intervalo pesquisável em vez de para o intervalo de reprodução.

      Qualquer interação do usuário para busca pode ser considerada segura no intervalo pesquisável.
   * Você pode implementar uma barra de controle que é mapeada para o intervalo de reprodução, mas que também exibe o intervalo pesquisável.

      Para uma barra de controle:
   1. Adicione uma sobreposição à barra de controle que representa o intervalo de reprodução.
   1. Quando o usuário start buscar, verifique se a posição de busca desejada está dentro do intervalo pesquisável usando `MediaPlayer.getSeekableRange`.

      Por exemplo:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      Você também pode optar por buscar o ponto ativo do cliente usando a constante `MediaPlayer.LIVE_POINT`.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```


