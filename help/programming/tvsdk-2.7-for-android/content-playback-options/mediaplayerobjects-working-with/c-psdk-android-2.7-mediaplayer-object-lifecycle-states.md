---
description: O status do player de mídia determina quais ações são legais.
seo-description: O status do player de mídia determina quais ações são legais.
seo-title: Ciclo de vida e status do objeto MediaPlayer
title: Ciclo de vida e status do objeto MediaPlayer
uuid: a0eb27c8-180b-4c56-926f-59fa3bcef032
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Ciclo de vida e status do objeto MediaPlayer {#lifecycle-and-statuses-of-the-mediaplayer-object}

O status do player de mídia determina quais ações são legais.

Para trabalhar com status de player de mídia:

* Você pode recuperar o status atual do objeto `MediaPlayer` com `MediaPlayer.getStatus()`.

* A lista de status é definida na enumeração [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/com/adobe/mediacore/MediaPlayerStatus.html).

Diagrama de transição de status para o ciclo de vida de uma instância `MediaPlayer`:
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
       <li id="li_08459A3AB03C45588D73FA162C27A56C">O <span class="codeph"> MediaPlayer </span> chama automaticamente <span class="codeph"> suspender </span> apenas quando o objeto de superfície utilizado pelo <span class="codeph"> MediaPlayerView </span> for destruído. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">O <span class="codeph"> MediaPlayer </span> chama automaticamente <span class="codeph"> restore() </span> apenas quando um novo objeto de superfície usado pelo <span class="codeph"> MediaPlayerView </span> é criado. </li> 
      </ul> </p> </p> <p>Se quiser que a reprodução sempre seja pausada quando o MediaPlayer for restaurado, faça com que sua chamada de aplicativo <span class="codeph"> MediaPlayer.pause() </span> no método Android Atividade <span class="codeph"> onPause() </span>. </p> </td> 
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
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que o aplicativo pode fazer a seguir. Para obter mais informações, consulte <a href="../../../tvsdk-2.7-for-android/content-playback-options/t-psdk-android-2.7-error-handling-set-up.md#set-up-error-handling" format="dita" scope="local"> Configurar a manipulação de erros </a>. </p> </td> 
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

