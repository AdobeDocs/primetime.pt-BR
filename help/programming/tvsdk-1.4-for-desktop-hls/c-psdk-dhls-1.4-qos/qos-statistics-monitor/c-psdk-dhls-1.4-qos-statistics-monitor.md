---
description: A QoS (Quality of Service, qualidade do serviço) oferece uma visão detalhada de como o mecanismo de vídeo está se saindo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
seo-description: A QoS (Quality of Service, qualidade do serviço) oferece uma visão detalhada de como o mecanismo de vídeo está se saindo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
seo-title: Estatísticas da qualidade dos serviços
title: Estatísticas da qualidade dos serviços
uuid: 5c9d09a9-0e0b-44f2-98ca-2eeb8a830ec6
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Estatísticas da qualidade dos serviços {#quality-of-service-statistics}

A QoS (Quality of Service, qualidade do serviço) oferece uma visão detalhada de como o mecanismo de vídeo está se saindo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.

O TVSDK também fornece informações sobre os seguintes recursos baixados:

* Arquivos de lista de reprodução/manifesto
* Fragmentos de arquivo
* Rastreamento de informações para arquivos

## Rastrear no nível do fragmento usando informações de carregamento {#track-at-the-fragment-level-using-load-information}

Você pode ler informações de qualidade de serviço (QoS) sobre recursos baixados, como fragmentos e rastreamentos, da classe LoadInformation.

1. Implemente o ouvinte de evento de `onLoadInformationAvailable` retorno de chamada.

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. Registre o ouvinte de eventos, que o TVSDK chama sempre que um fragmento é baixado.

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. Leia os dados de interesse do `LoadInformation` que é passado para o retorno de chamada.

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> Propriedade </th> 
      <th colname="col1" class="entry"> Tipo </th> 
      <th colname="col2" class="entry"> Descrição </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> <p>A duração do download em milissegundos. </p> <p>O TVSDK não diferencia entre o tempo que o cliente levou para se conectar ao servidor e o tempo que levou para baixar o fragmento completo. Por exemplo, se um segmento de 10 MB levar 8 segundos para ser baixado, o TVSDK fornece essas informações, mas não informa que levou 4 segundos até o primeiro byte e outros 4 segundos para baixar o fragmento inteiro. </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> A duração da mídia dos fragmentos baixados em milissegundos. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> tamanho </span> </td> 
      <td colname="col1"> <p>Número </p> </td> 
      <td colname="col2"> O tamanho do recurso baixado em bytes. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> O índice da via correspondente, se for conhecido; caso contrário, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O nome da faixa correspondente, se for conhecido; caso contrário, nulo. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O tipo da via correspondente, se conhecida; caso contrário, nulo. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O que o TVSDK baixou. Um dos seguintes: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFESTO - Uma lista de reprodução/manifesto </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENTO - Um fragmento </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK - Um fragmento associado a um rastreamento específico </li> 
      </ul> Às vezes, talvez não seja possível detectar o tipo de recurso. Se isso ocorrer, FILE será retornado. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O URL que aponta para o recurso baixado. </td> 
   </tr> 
   </tbody> 
   </table>

## Leia as estatísticas de reprodução, buffering e dispositivo do QOS {#read-qos-playback-buffering-and-device-statistics}

Você pode ler as estatísticas de reprodução, buffering e dispositivo da classe QOSProvider.

A `QOSProvider` classe fornece várias estatísticas, incluindo informações sobre buffering, taxas de bits, taxas de quadros, dados de tempo e assim por diante.

Ele também fornece informações sobre o dispositivo, como fabricante, modelo, sistema operacional, versão do SDK e tamanho/densidade da tela.

1. Instanciar um player de mídia.
1. Crie um `QOSProvider` objeto e anexe-o ao player de mídia.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Leia as estatísticas de reprodução.

   Uma solução para ler as estatísticas de reprodução é ter um timer, que periodicamente obtém os novos valores de QoS do `QOSProvider`. Por exemplo:

   ```
   var qosTimer:Timer = new Timer(1000); // every 1 second  
   qosTimer.addEventListener(TimerEvent.Timer, onQoSTimer);  
   qosTimer.start(); 
   private function onQoSTimer(event:TimerEvent):void { 
       var playbackInformation:PlaybackInformation = _mediaQosProvider.getPlaybackInformation(); 
       qosInfo["Frame rate"] = playbackInformation.frameRate.toFixed();  
       qosInfo["Dropped frames"] = playbackInformation.droppedFrameCount.toFixed(); 
       qosInfo["Bitrate"] = playbackInformation.bitrate.toFixed(); 
       qosInfo["Bandwidth"] = playbackInformation.perceivedBandwidth; 
       qosInfo["Buffering time"] = playbackInformation.bufferingTime.toFixed(); 
       qosInfo["Buffer length"] = playbackInformation.bufferLength.toFixed();  
       qosInfo["Buffer time"] = playbackInformation.bufferTime.toFixed(); 
       qosInfo["Empty buffer count"] = playbackInformation.emptyBufferCount.toFixed();  
       qosInfo["Time to load"] = playbackInformation.timeToLoad.toFixed();  
       qosInfo["Time to start"] = playbackInformation.timeToStart.toFixed(); 
       qosView.update(qosInfo); 
   }
   ```

1. (Opcional) Leia as informações específicas do dispositivo.

   ```
   // Show device information 
   var deviceInfo:DeviceInformation = new QOSProvider.deviceInformation; 
   qosInfo["deviceModel"] = deviceInfo.manufacturer +"-" + deviceInfo.model; 
   qosInfo["os"] = deviceInfo.os;  
   qosInfo["runtime"] = deviceInfo.runtimeVersion;  
   qosInfo["widthPixels"] = deviceInfo.widthPixels;  
   qosInfo["heightPixels"] = deviceInfo.heightPixels; 
   qosView.update(qosInfo); 
   ```
