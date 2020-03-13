---
description: O objeto PTMediaPlayer representa o player de mídia. Um PTMediaPlayerItem representa áudio ou vídeo no player.
seo-description: O objeto PTMediaPlayer representa o player de mídia. Um PTMediaPlayerItem representa áudio ou vídeo no player.
seo-title: Trabalhar com objetos MediaPlayer
title: Trabalhar com objetos MediaPlayer
uuid: 0c33ebd6-b11a-4e62-8c1c-880cfceff474
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Trabalhar com objetos MediaPlayer {#work-with-mediaplayer-objects}

O objeto PTMediaPlayer representa o player de mídia. Um PTMediaPlayerItem representa áudio ou vídeo no player.

## Sobre a classe MediaPlayerItem {#section_B6F36C0462644F5C932C8AA2F6827071}

Depois que um recurso de mídia é carregado com êxito, o TVSDK cria uma instância da `PTMediaPlayerItem` classe para fornecer acesso a esse recurso.

O `PTMediaPlayer` resolve o recurso de mídia, carrega o arquivo manifest associado e analisa o manifesto. Esta é a parte assíncrona do processo de carregamento de recursos. A `PTMediaPlayerItem` instância é produzida depois que o recurso é resolvido, e essa instância é uma versão resolvida de um recurso de mídia. O TVSDK fornece acesso à `PTMediaPlayerItem` instância recém-criada por meio `PTMediaPlayer.currentItem`.

>[!TIP]
>
>É necessário aguardar o carregamento do recurso com êxito antes de acessar o item do player de mídia.

## Ciclo de vida do objeto MediaPlayer {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

A partir do momento em que você cria a `PTMediaPlayer` instância até o momento em que a encerra (reutiliza ou remove), essa instância conclui uma série de transições de um status para outro.

Algumas operações são permitidas apenas quando o player está em um estado específico. Por exemplo, chamar `play` não `PTMediaPlayerStatusCreated` é permitido. Você pode chamar esse status somente depois que o player atingir o `PTMediaPlayerStatusReady` status.

Para trabalhar com status:

* Você pode recuperar o status atual do objeto MediaPlayer com `PTMediaPlayer.status`.
* A lista de status é definida em `PTMediaPlayerStatus`.

Diagrama de transição de estado para o ciclo de vida de uma instância do MediaPlayer:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

A tabela a seguir fornece detalhes adicionais:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>PTMediaPlayerStatus</b></th> 
   <th colname="col2" class="entry"><b>Ocorre quando</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>Seu aplicativo solicitou um novo player de mídia chamando <span class="codeph"> playerWithMediaPlayerItem</span>. O player recém-criado está aguardando que você especifique um item de player de mídia. Este é o status inicial do player de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>Seu aplicativo chama <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>e o player de mídia está sendo carregado. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>O TVSDK definiu com êxito o item do player de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>O conteúdo é preparado e os anúncios foram inseridos na linha do tempo ou o procedimento do anúncio falhou. O buffer ou a reprodução podem começar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> play</span>, portanto, o TVSDK está tentando reproduzir o vídeo. Alguns buffering podem ocorrer antes que o vídeo seja reproduzido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>Conforme seu aplicativo reproduz e pausa a mídia, o player de mídia se move entre esse estado e <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>O player atingiu o fim do fluxo e a reprodução parou. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>Seu aplicativo lançou o media player, que também libera todos os recursos associados. Você não pode mais usar esta instância </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que seu aplicativo pode fazer a seguir. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Você pode usar o status para fornecer feedback sobre o processo (por exemplo, uma roleta enquanto espera pela próxima alteração de status) ou para executar a mídia, como aguardar o status apropriado antes de chamar o próximo método.