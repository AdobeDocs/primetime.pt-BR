---
description: A Qualidade do serviço (QoS) oferece uma visualização detalhada do desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
title: Estatísticas de qualidade do serviço
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Estatísticas de qualidade do serviço {#quality-of-service-statistics}

A Qualidade do serviço (QoS) oferece uma visualização detalhada do desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.

O TVSDK também fornece informações sobre os seguintes recursos baixados:

* Arquivos de lista de reprodução/manifesto
* Fragmentos de arquivo
* Informações de rastreamento para arquivos

## Rastrear no nível do fragmento usando informações de carregamento {#track-at-the-fragment-level-using-load-information}

Você pode ler informações de qualidade de serviço (QoS) sobre recursos baixados, como fragmentos e rastreamentos, a partir da classe LoadInformation.

1. Implementar o `onLoadInformationAvailable` ouvinte de eventos de retorno de chamada.

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

1. Leia os dados de interesse no `LoadInformation` que é passado para o retorno de chamada.

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
      <td colname="col2"> <p>A duração do download em milissegundos. </p> <p>O TVSDK não diferencia entre o tempo necessário para o cliente se conectar ao servidor e o tempo necessário para baixar o fragmento completo. Por exemplo, se um segmento de 10 MB levar 8 segundos para baixar, o TVSDK fornecerá essas informações, mas não informará que levou 4 segundos até o primeiro byte e outros 4 segundos para baixar o fragmento inteiro. </p> </td> 
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
      <td colname="col2"> O índice da faixa correspondente, se conhecido; caso contrário, 0. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O nome da faixa correspondente, se for conhecido; caso contrário, é nulo. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O tipo da faixa correspondente, se conhecida; caso contrário, é nulo. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O que o TVSDK baixou. Uma das seguintes opções: 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFESTO - Uma lista de reprodução/manifesto </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">FRAGMENTO - Um fragmento </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">RASTREAR - Um fragmento associado a uma faixa específica </li> 
      </ul> Às vezes, pode não ser possível detectar o tipo do recurso. Se isso ocorrer, FILE será retornado. </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>String </p> </td> 
      <td colname="col2"> O URL que aponta para o recurso baixado. </td> 
   </tr> 
   </tbody> 
   </table>

## Ler estatísticas de reprodução, buffering e dispositivo de QOS {#read-qos-playback-buffering-and-device-statistics}

Você pode ler estatísticas de reprodução, buffering e dispositivo na classe QOSProvider.

A variável `QOSProvider` A classe fornece várias estatísticas, incluindo informações sobre buffering, taxas de bits, taxas de quadros, dados de tempo, etc.

Também fornece informações sobre o dispositivo, como fabricante, modelo, sistema operacional, versão do SDK e tamanho/densidade da tela.

1. Instanciar um reprodutor de mídia.
1. Criar um `QOSProvider` e anexe-o ao reprodutor de mídia.

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Leia as estatísticas de reprodução.

   Uma solução para ler as estatísticas de reprodução é ter um temporizador, que busca periodicamente os novos valores de QoS na `QOSProvider`. Por exemplo:

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
