---
description: A partir do momento em que você cria a instância MediaPlayer até o momento em que a encerra (reutilize ou remova), essa instância conclui uma série de transições entre estados.
title: Ciclo de vida do objeto MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Ciclo de vida do objeto MediaPlayer{#mediaplayer-object-lifecycle}

A partir do momento em que você cria a instância MediaPlayer até o momento em que a encerra (reutilize ou remova), essa instância conclui uma série de transições entre estados.

Algumas operações são permitidas somente quando o reprodutor está em um estado específico. Por exemplo, chamar `play` em `IDLE` não é permitido. Você pode chamar esse status somente depois que o reprodutor atingir o estado `PREPARED`.

Para trabalhar com estados:

* Você pode recuperar o estado atual do objeto `MediaPlayer` com `MediaPlayer.getStatus`.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* A lista de estados é definida em `MediaPlayer.PlayerState`.

Diagrama de transição de estado para o ciclo de vida de uma instância `MediaPlayer`:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

A tabela a seguir fornece detalhes adicionais:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> Ocorre quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> OCIOSO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo solicitou um novo reprodutor de mídia, chamando <span class="codeph"> DefaultMediaPlayer.create </span>. O reprodutor recém-criado está aguardando que você especifique um item de reprodutor de mídia. Este é o estado inicial do reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZAÇÃO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> MediaPlayer.replaceCurrentItem </span> e o reprodutor de mídia está carregando. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZADO  </span> </td> 
   <td colname="col2"> <p>TVSDK definiu com êxito o item do reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARAÇÃO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> MediaPlayer.prepareToPlay </span>. O reprodutor de mídia está carregando o item do reprodutor de mídia e os recursos associados. </p> <p>Dica:  Pode ocorrer algum buffering da mídia principal. </p> <p>O TVSDK está preparando o fluxo de mídia e tentando executar a resolução do anúncio e a inserção do anúncio (se ativada). </p> <p>Dica:  Para definir a hora de início com um valor diferente de zero, chame <span class="codeph"> prepareToPlay(startTime) </span> com a hora em milissegundos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARADO  </span> </td> 
   <td colname="col2"> <p>O conteúdo é preparado e os anúncios foram inseridos na linha do tempo, ou o procedimento do anúncio falhou. O buffering ou a reprodução podem começar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> REPRODUÇÃO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> de reprodução </span>, portanto, TVSDK está tentando reproduzir o vídeo. Alguns buffering podem ocorrer antes que o vídeo seja reproduzido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PAUSADO  </span> </td> 
   <td colname="col2"> <p>Conforme seu aplicativo reproduz e pausa a mídia, o reprodutor de mídia se move entre esse estado e REPRODUZINDO. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SUSPENSA  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo saiu da reprodução, desligou o dispositivo ou mudou os aplicativos enquanto o reprodutor estava sendo reproduzido ou pausado. O reprodutor de mídia foi suspenso e os recursos foram liberados. Para continuar, restaure o reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETE  </span> </td> 
   <td colname="col2"> <p>O reprodutor atingiu o fim do fluxo e a reprodução parou. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> LANÇADO  </span> </td> 
   <td colname="col2"> <p>Seu aplicativo lançou o reprodutor de mídia, que também lança todos os recursos associados. Não é mais possível usar essa instância </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERRO  </span> </td> 
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que seu aplicativo pode fazer em seguida. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Você pode usar o estado para fornecer feedback sobre o processo (por exemplo, um ponteiro enquanto aguarda a próxima alteração de estado) ou para dar a próxima etapa na reprodução da mídia, como aguardar o estado apropriado antes de chamar o próximo método.

Por exemplo:

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```

