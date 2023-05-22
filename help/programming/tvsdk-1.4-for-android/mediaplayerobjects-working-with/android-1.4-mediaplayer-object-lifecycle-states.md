---
description: A partir do momento em que você cria a ocorrência de MediaPlayer até o momento em que você a encerra (reutiliza ou remove), essa ocorrência conclui uma série de transições entre estados.
title: Ciclo de vida do objeto MediaPlayer
exl-id: efb39fea-1050-41e5-93d8-1175a54f81e5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Ciclo de vida do objeto MediaPlayer{#mediaplayer-object-lifecycle}

A partir do momento em que você cria a ocorrência de MediaPlayer até o momento em que você a encerra (reutiliza ou remove), essa ocorrência conclui uma série de transições entre estados.

Algumas operações são permitidas somente quando o reprodutor está em um estado específico. Por exemplo, chamar `play` in `IDLE` não é permitido. Você pode chamar esse status somente depois que o reprodutor atingir a `PREPARED` estado.

Para trabalhar com estados:

* Você pode recuperar o estado atual do `MediaPlayer` objeto com `MediaPlayer.getStatus`.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* A lista de estados é definida em `MediaPlayer.PlayerState`.

Diagrama de transição de estado para o ciclo de vida de um `MediaPlayer` instância:
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
   <td colname="col2"> <p>Seu aplicativo solicitou um novo reprodutor de mídia chamando <span class="codeph"> DefaultMediaPlayer.create </span>. O reprodutor recém-criado está aguardando que você especifique um item de reprodutor de mídia. Esse é o estado inicial do reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZANDO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> MediaPlayer.replaceCurrentItem </span>e o reprodutor de mídia está carregando. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INICIALIZADO </span> </td> 
   <td colname="col2"> <p>O TVSDK definiu com êxito o item do reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARANDO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> MediaPlayer.prepareToPlay </span>. O reprodutor de mídia está carregando o item de reprodutor de mídia e os recursos associados. </p> <p>Dica: pode ocorrer algum buffering na mídia principal. </p> <p>O TVSDK está preparando o fluxo de mídia e tentando executar a resolução e a inserção de anúncios (se habilitada). </p> <p>Dica: para definir a hora de início como um valor diferente de zero, chame <span class="codeph"> prepareToPlay(startTime) </span> com o tempo em milissegundos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARADO </span> </td> 
   <td colname="col2"> <p>O conteúdo está preparado e os anúncios foram inseridos na linha do tempo, ou o procedimento de publicidade falhou. O buffering ou a reprodução podem começar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> REPRODUÇÃO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo chamou <span class="codeph"> play </span>, portanto, o TVSDK está tentando reproduzir o vídeo. Alguns buffering pode ocorrer antes que o vídeo seja reproduzido. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PAUSADO </span> </td> 
   <td colname="col2"> <p>À medida que o aplicativo é reproduzido e pausa a mídia, o reprodutor de mídia se move entre esse estado e a função REPRODUZINDO. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SUSPENSO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo saiu da reprodução, desligou o dispositivo ou trocou de aplicativo enquanto o reprodutor estava sendo reproduzido ou pausado. O reprodutor de mídia foi suspenso e os recursos foram liberados. Para continuar, restaure o reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> CONCLUÍDO </span> </td> 
   <td colname="col2"> <p>O reprodutor atingiu o fim do fluxo e a reprodução foi interrompida. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> LANÇADO </span> </td> 
   <td colname="col2"> <p>Seu aplicativo lançou o reprodutor de mídia, que também libera os recursos associados. Não é mais possível usar esta instância </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERRO </span> </td> 
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que o aplicativo pode fazer a seguir. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Você pode usar o estado para fornecer feedback sobre o processo (por exemplo, um ponteiro enquanto aguarda a próxima alteração de estado) ou para dar o próximo passo na reprodução da mídia, como aguardar o estado apropriado antes de chamar o próximo método.

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
