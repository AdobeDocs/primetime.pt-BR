---
description: A partir do momento em que você cria a instância do MediaPlayer até o momento em que a encerra (reutiliza ou remove), essa instância conclui uma série de transições entre estados.
seo-description: A partir do momento em que você cria a instância do MediaPlayer até o momento em que a encerra (reutiliza ou remove), essa instância conclui uma série de transições entre estados.
seo-title: Ciclo de vida do objeto MediaPlayer
title: Ciclo de vida do objeto MediaPlayer
uuid: 6670a30c-7053-4754-bc36-6bb8590c001d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Ciclo de vida do objeto MediaPlayer{#mediaplayer-object-lifecycle}

A partir do momento em que você cria a instância do MediaPlayer até o momento em que a encerra (reutiliza ou remove), essa instância conclui uma série de transições entre estados.

Algumas operações são permitidas apenas quando o player está em um estado específico. Por exemplo, chamar `play` não `IDLE` é permitido. Você pode chamar esse status somente depois que o player chegar ao `PREPARED` estado.

Para trabalhar com estados:

* Você pode recuperar o estado atual do `MediaPlayer` objeto com `MediaPlayer.getStatus`.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* A lista de estados é definida em `MediaPlayer.PlayerState`.

Diagrama de transição de estado para o ciclo de vida de uma `MediaPlayer` instância:
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
   <td colname="col1"> <span class="codeph"> OCIOSO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo solicitou um novo player de mídia chamando <span class="codeph"> DefaultMediaPlayer.create </span>. O player recém-criado está aguardando que você especifique um item de player de mídia. Este é o estado inicial do media player. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZAÇÃO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamado <span class="codeph"> MediaPlayer.replaceCurrentItem </span>, e o player de mídia está sendo carregado. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZADO </span> </td> 
   <td colname="col2"> <p>O TVSDK definiu com êxito o item do player de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARANDO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> MediaPlayer.prepareToPlay </span>. O media player está carregando o item do media player e os recursos associados. </p> <p>Dica:  Pode ocorrer algum buffering da mídia principal. </p> <p>O TVSDK está preparando o fluxo de mídia e tentando executar a resolução de anúncios e a inserção de anúncios (se ativada). </p> <p>Dica:  Para definir a hora de início como um valor diferente de zero, chame <span class="codeph"> prepareToPlay(startTime) </span> com o tempo em milissegundos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARADO </span> </td> 
   <td colname="col2"> <p>O conteúdo é preparado e os anúncios foram inseridos na linha do tempo ou o procedimento do anúncio falhou. O buffer ou a reprodução podem começar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> REPRODUÇÃO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> play </span>, então o TVSDK está tentando reproduzir o vídeo. Alguns buffering podem ocorrer antes que o vídeo seja reproduzido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PAUSADO </span> </td> 
   <td colname="col2"> <p>À medida que seu aplicativo reproduz e pausa a mídia, o player de mídia se move entre esse estado e REPRODUZINDO. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SUSPENSA </span> </td> 
   <td colname="col2"> <p>Seu aplicativo saiu da reprodução, encerrou o dispositivo ou comutou aplicativos enquanto o player estava sendo reproduzido ou pausado. O media player foi suspenso e os recursos foram liberados. Para continuar, restaure o player de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> CONCLUÍDO </span> </td> 
   <td colname="col2"> <p>O player atingiu o fim do fluxo e a reprodução parou. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> LANÇADO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo lançou o media player, que também libera todos os recursos associados. Você não pode mais usar esta instância </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERRO </span> </td> 
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que seu aplicativo pode fazer a seguir. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Você pode usar o estado para fornecer feedback sobre o processo (por exemplo, uma roleta enquanto espera pela próxima alteração de estado) ou para executar a mídia, como aguardar o estado apropriado antes de chamar o próximo método.

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

