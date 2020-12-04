---
description: A partir do momento em que você cria a instância do MediaPlayer até o momento em que a encerra (reutilize ou remova), essa instância conclui uma série de transições entre os status.
seo-description: A partir do momento em que você cria a instância do MediaPlayer até o momento em que a encerra (reutilize ou remova), essa instância conclui uma série de transições entre os status.
seo-title: Ciclo de vida do objeto MediaPlayer
title: Ciclo de vida do objeto MediaPlayer
uuid: 1452ae3a-7ce9-439e-951c-9d3db63b1d20
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# Ciclo de vida do objeto MediaPlayer{#mediaplayer-object-lifecycle}

A partir do momento em que você cria a instância do MediaPlayer até o momento em que a encerra (reutilize ou remova), essa instância conclui uma série de transições entre os status.

Algumas operações são permitidas apenas quando o player está em um estado específico. Por exemplo, chamar `play` no IDLE não é permitido. Você pode chamar esse status somente depois que o player atingir o estado PREPARADO.

Para trabalhar com status:

* Você pode recuperar o estado atual do objeto `MediaPlayer` usando a propriedade `MediaPlayer.status`.

   ```
   function get status():String;
   ```

* A lista de status é definida em `MediaPlayer.PlayerStatus`.

Diagrama de transição de estado para o ciclo de vida de uma instância `MediaPlayer`:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

A tabela a seguir fornece detalhes adicionais:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus  </span> </th> 
   <th colname="col2" class="entry"> Ocorre quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> OCIOSO  </span> </td> 
   <td colname="col2"> <p> Seu aplicativo solicitou um novo player de mídia instanciando <span class="codeph"> o MediaPlayer </span>. O player recém-criado está aguardando que você especifique um item de player de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZAÇÃO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamado <span class="codeph"> MediaPlayer.replaceCurrentResource </span> e o player de mídia está sendo carregado. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZADO  </span> </td> 
   <td colname="col2"> <p>O TVSDK definiu com êxito o item do player de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARANDO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> MediaPlayer.prepareToPlay </span>. O media player está carregando o item do media player e os recursos associados. </p> <p>Dica:  Pode ocorrer algum buffering da mídia principal. </p> <p>O TVSDK está preparando o fluxo de mídia e tentando executar a resolução de anúncios e a inserção de anúncios (se ativada). </p> <p>Dica:  Para definir a hora do start com um valor diferente de zero, chame <span class="codeph"> prepareToPlay(startTime) </span> com a hora em milésimos de segundo. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARADO  </span> </td> 
   <td colname="col2"> <p>O conteúdo é preparado e os anúncios foram inseridos na linha do tempo ou o procedimento do anúncio falhou. O buffer ou a reprodução podem começar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> REPRODUÇÃO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> play </span>, portanto, o TVSDK está tentando reproduzir o vídeo. Alguns buffering podem ocorrer antes que o vídeo seja reproduzido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PAUSADO  </span> </td> 
   <td colname="col2"> <p>À medida que seu aplicativo reproduz e pausa a mídia, o player de mídia se move entre esse estado e REPRODUZINDO. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PROCURANDO  </span> </td> 
   <td colname="col2"> <p>O player de mídia está buscando a posição correta durante a pausa ou reprodução. Para determinar quando a busca foi iniciada ou encerrada, ouça os eventos <span class="codeph"> SeekEvent.SEEK_BEGIN </span> e <span class="codeph"> SeekEvent.SEEK_END </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> CONCLUÍDO  </span> </td> 
   <td colname="col2"> <p>O player atingiu o fim do fluxo e a reprodução parou. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> LANÇADO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo lançou o media player, que também libera todos os recursos associados. Você não pode mais usar esta instância </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERRO  </span> </td> 
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que seu aplicativo pode fazer a seguir. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Você pode usar o status para fornecer feedback sobre o processo (por exemplo, uma roleta enquanto espera pela próxima alteração de status) ou para executar a mídia, como aguardar o status apropriado antes de chamar o próximo método.

