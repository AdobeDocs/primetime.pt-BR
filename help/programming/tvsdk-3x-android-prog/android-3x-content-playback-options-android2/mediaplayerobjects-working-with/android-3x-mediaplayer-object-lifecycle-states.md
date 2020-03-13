---
description: O status do player de mídia determina quais ações são legais.
seo-description: O status do player de mídia determina quais ações são legais.
seo-title: Ciclo de vida e status do objeto MediaPlayer
title: Ciclo de vida e status do objeto MediaPlayer
uuid: a2866f84-a722-46ed-b4cb-36664db5be82
translation-type: tm+mt
source-git-commit: 56dc79e5b4df11ff730d7d8f23dea8d0f4712077

---


# Ciclo de vida e status do objeto MediaPlayer{#lifecycle-and-statuses-of-the-mediaplayer-object}

O status do player de mídia determina quais ações são legais.

Para trabalhar com status de player de mídia:

* É possível recuperar o status atual do `MediaPlayer` objeto com `MediaPlayer.getStatus()`.

* A lista de status é definida na enumeração [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html) .

Diagrama de transição de status para o ciclo de vida de uma `MediaPlayer` instância:

<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

A tabela a seguir fornece detalhes sobre o ciclo de vida e os status do player de mídia:

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Status </th> 
   <th colname="col2" class="entry"> Ocorre quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> OCIOSO </td> 
   <td colname="col2"> <p>O status inicial do player de mídia. O player é criado e está aguardando que você especifique um item de player de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INICIALIZAÇÃO </td> 
   <td colname="col2"> <p>Seu aplicativo chama <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>O item do media player está sendo carregado. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INICIALIZADO </td> 
   <td colname="col2"> <p>O TVSDK definiu com êxito o item media-player. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARANDO </td> 
   <td colname="col2"> <p>Seu aplicativo chama <span class="codeph"> MediaPlayer.prepareToPlay() </span>. O media player está carregando o item do media player e quaisquer recursos associados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARADO </td> 
   <td colname="col2"> <p>O TVSDK preparou o fluxo de mídia e tentou executar a resolução de anúncios e a inserção de anúncios (se ativada). O conteúdo é preparado e os anúncios foram inseridos na linha do tempo ou o procedimento do anúncio falhou. </p> <p>O buffer ou a reprodução podem começar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> REPRODUÇÃO/PAUSA </td> 
   <td colname="col2"> <p>À medida que o aplicativo reproduz e pausa a mídia, o player de mídia se move entre esses status. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SUSPENSA </td> 
   <td colname="col2"> <p>Se o aplicativo sair da reprodução, desligar o dispositivo ou alternar aplicativos enquanto o player estiver sendo reproduzido ou pausado, o player de mídia será suspenso e os recursos serão liberados. </p> <p>Chamar <span class="codeph"> MediaPlayer.restore() </span> retorna o player ao status em que ele estava antes de SUSPENDER. A exceção é se o player estiver PROCURANDO quando suspenso, ele será PAUSADO e SUSPENDIDO. </p> <p>Importante:  <p>Lembre-se das seguintes informações: 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">O <span class="codeph"> MediaPlayer </span> chama <span class="codeph"> a suspensão automaticamente </span> somente quando o objeto de superfície usado pelo <span class="codeph"> MediaPlayerView </span> é destruído. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">O <span class="codeph"> MediaPlayer </span> chama <span class="codeph"> restore() automaticamente </span> somente quando um novo objeto de superfície usado pelo <span class="codeph"> MediaPlayerView </span> é criado. </li> 
      </ul> </p> </p> <p>Se você quiser que a reprodução sempre seja pausada quando o MediaPlayer for restaurado, faça com que seu aplicativo chame <span class="codeph"> MediaPlayer.pause() </span> no método <span class="codeph"> onPause() do Android Activity </span> . </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> CONCLUÍDO </td> 
   <td colname="col2"> <p>O player chegou ao fim do fluxo e a reprodução parou. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> LANÇADO </td> 
   <td colname="col2"> <p>Seu aplicativo lançou o media player, que também libera todos os recursos associados. Não é mais possível usar essa instância. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ERRO </td> 
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que o aplicativo pode fazer a seguir. Para obter mais informações, consulte <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local"> Configurar a manipulação de erros </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Você pode usar o status para fornecer feedback sobre o processo, por exemplo, uma roleta enquanto aguarda a próxima alteração de status, ou executar as próximas etapas da mídia, como aguardar o status apropriado antes de chamar o próximo método.

Por exemplo:

```java
mediaPlayer.addEventListener(MediaPlayerEvent STATUS_CHANGED, new StatusChangeEventListener() { 
    @Override  
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        switch(event.getStatus()) { 
            case INITIALIZED: 
                mediaPlayer.prepareToPlay(); 
                break; 
            case PREPARING: 
                showBufferingSpinner(); 
                break; 
            case PREPARED: 
                hideBufferingSpinner(); 
                mediaPlayer.play(); 
                break; 
            ...                
        } 
        ... 
    } 
}); 
```
