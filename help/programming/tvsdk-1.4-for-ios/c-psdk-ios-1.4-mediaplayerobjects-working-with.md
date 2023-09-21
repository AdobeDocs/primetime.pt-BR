---
description: O objeto PTMediaPlayer representa o reprodutor de mídia. Um PTMediaPlayerItem representa áudio ou vídeo no player.
title: Trabalhar com objetos MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Trabalhar com objetos MediaPlayer{#work-with-mediaplayer-objects}

O objeto PTMediaPlayer representa o reprodutor de mídia. Um PTMediaPlayerItem representa áudio ou vídeo no player.

## Sobre a classe MediaPlayerItem {#section_B6F36C0462644F5C932C8AA2F6827071}

Depois que um recurso de mídia é carregado com êxito, o TVSDK cria uma instância do `PTMediaPlayerItem` para fornecer acesso a esse recurso.

A variável `PTMediaPlayer` resolve o recurso de mídia, carrega o arquivo de manifesto associado e analisa o manifesto. Essa é a parte assíncrona do processo de carregamento de recursos. A variável `PTMediaPlayerItem` A instância é produzida após o recurso ser resolvido e essa instância é uma versão resolvida de um recurso de mídia. O TVSDK fornece acesso ao recém-criado `PTMediaPlayerItem` instância por meio de `PTMediaPlayer.currentItem`.

>[!TIP]
>
>Aguarde até que o recurso seja carregado com êxito antes de acessar o item do reprodutor de mídia.

## Ciclo de vida do objeto MediaPlayer {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

A partir do momento em que você cria a variável `PTMediaPlayer` até o momento em que você a encerra (reutiliza ou remove), essa instância conclui uma série de transições de um status para outro.

Algumas operações são permitidas somente quando o reprodutor está em um estado específico. Por exemplo, chamar `play` in `PTMediaPlayerStatusCreated` não é permitido. Você pode chamar esse status somente depois que o reprodutor atingir a `PTMediaPlayerStatusReady` status.

Para trabalhar com status:

* Você pode recuperar o status atual do objeto MediaPlayer com `PTMediaPlayer.status`.
* A lista de status é definida em `PTMediaPlayerStatus`.

Diagrama de transição de estado do ciclo de vida de uma ocorrência de MediaPlayer:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

A tabela a seguir fornece detalhes adicionais:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> PTMediaPlayerStatus </th> 
   <th colname="col2" class="entry"> Ocorre quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>Seu aplicativo solicitou um novo reprodutor de mídia chamando <span class="codeph"> playerWithMediaPlayerItem</span>. O reprodutor recém-criado está aguardando que você especifique um item de reprodutor de mídia. Este é o status inicial do reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>Suas chamadas de aplicativo <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>e o reprodutor de mídia está carregando. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>O TVSDK definiu com êxito o item do reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>O conteúdo está preparado e os anúncios foram inseridos na linha do tempo, ou o procedimento de publicidade falhou. O buffering ou a reprodução podem começar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> play</span>, portanto, o TVSDK está tentando reproduzir o vídeo. Alguns buffering pode ocorrer antes que o vídeo seja reproduzido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>À medida que o aplicativo reproduz e pausa a mídia, o reprodutor de mídia se move entre esse estado e <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>O reprodutor atingiu o fim do fluxo e a reprodução foi interrompida. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>Seu aplicativo lançou o reprodutor de mídia, que também libera os recursos associados. Não é mais possível usar esta instância </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que o aplicativo pode fazer a seguir. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Você pode usar o status para fornecer feedback sobre o processo (por exemplo, um ponteiro enquanto aguarda a próxima alteração de status) ou para dar o próximo passo na reprodução da mídia, como aguardar o status apropriado antes de chamar o próximo método.
