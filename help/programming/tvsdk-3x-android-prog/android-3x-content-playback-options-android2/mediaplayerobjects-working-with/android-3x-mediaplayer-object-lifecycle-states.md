---
description: O status do reprodutor de mídia determina quais ações são legais.
title: Ciclo de vida e status do objeto MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Ciclo de vida e status do objeto MediaPlayer{#lifecycle-and-statuses-of-the-mediaplayer-object}

O status do reprodutor de mídia determina quais ações são legais.

Para trabalhar com status do reprodutor de mídia:

* Você pode recuperar o status atual da `MediaPlayer` objeto com `MediaPlayer.getStatus()`.

* A lista de status é definida no campo [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html) enum.

Diagrama de transição de status para o ciclo de vida de um `MediaPlayer` instância:

<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

A tabela a seguir fornece detalhes sobre o ciclo de vida e os status do reprodutor de mídia:

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
   <td colname="col2"> <p>O status inicial do reprodutor de mídia. O reprodutor é criado e aguarda que você especifique um item de reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INICIALIZANDO </td> 
   <td colname="col2"> <p>Suas chamadas de aplicativo <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>O item do reprodutor de mídia está sendo carregado. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INICIALIZADO </td> 
   <td colname="col2"> <p>O TVSDK definiu com êxito o item do reprodutor de mídia. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARANDO </td> 
   <td colname="col2"> <p>Suas chamadas de aplicativo <span class="codeph"> MediaPlayer.prepareToPlay() </span>. O reprodutor de mídia está carregando o item do reprodutor de mídia e todos os recursos associados. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARADO </td> 
   <td colname="col2"> <p>O TVSDK preparou o fluxo de mídia e tentou executar a resolução e a inserção de anúncios (se estiver habilitado). O conteúdo é preparado e os anúncios foram inseridos na linha do tempo, ou o procedimento de anúncio falhou. </p> <p>O buffering ou a reprodução podem começar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> REPRODUÇÃO/PAUSADO </td> 
   <td colname="col2"> <p>À medida que o aplicativo reproduz e pausa a mídia, o reprodutor de mídia se move entre esses status. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SUSPENSO </td> 
   <td colname="col2"> <p>Se o aplicativo sair da reprodução, desligar o dispositivo ou alternar aplicativos enquanto o reprodutor está sendo reproduzido ou pausado, o reprodutor de mídia será suspenso e os recursos serão liberados. </p> <p>Chamando <span class="codeph"> MediaPlayer.restore() </span> retorna o reprodutor ao status em que ele estava antes de ser SUSPENSO. A exceção é se o reprodutor estiver BUSCANDO quando suspenso for chamado, o reprodutor for PAUSADO e depois SUSPENSO. </p> <p>Importante:  <p>Lembre-se das seguintes informações: 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">A variável <span class="codeph"> MediaPlayer </span> chama automaticamente <span class="codeph"> suspender </span> somente quando o objeto de superfície usado pelo <span class="codeph"> MediaPlayerView </span> é destruído. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">A variável <span class="codeph"> MediaPlayer </span> chama automaticamente <span class="codeph"> restore() </span> somente quando um novo objeto de superfície é usado pelo <span class="codeph"> MediaPlayerView </span> é criado. </li> 
      </ul> </p> </p> <p>Se quiser que a reprodução seja sempre pausada quando o MediaPlayer for restaurado, peça para o aplicativo chamar <span class="codeph"> MediaPlayer.pause() </span> no Guia de atividades do Android <span class="codeph"> onPause() </span> método. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> CONCLUÍDO </td> 
   <td colname="col2"> <p>O reprodutor atingiu o fim do fluxo e a reprodução foi interrompida. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> LANÇADO </td> 
   <td colname="col2"> <p>Seu aplicativo liberou o reprodutor de mídia, que também libera os recursos associados. Você não pode mais usar essa instância. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ERRO </td> 
   <td colname="col2"> <p>Ocorreu um erro durante o processo. Um erro também pode afetar o que o aplicativo pode fazer a seguir. Para obter mais informações, consulte <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local"> Configurar tratamento de erros </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Você pode usar o status para fornecer feedback sobre o processo, por exemplo, um ponteiro enquanto aguarda a próxima alteração de status, ou dar os próximos passos para reproduzir a mídia, como aguardar o status apropriado antes de chamar o próximo método.

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
