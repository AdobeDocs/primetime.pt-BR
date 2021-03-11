---
description: A Qualidade do serviço (QoS) oferece uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK do navegador fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
title: Estatísticas de qualidade dos serviços
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---


# Estatísticas de qualidade do serviço{#quality-of-service-statistics}

A Qualidade do serviço (QoS) oferece uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK do navegador fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.

## Ler a reprodução do QOS, o buffering e as estatísticas do dispositivo {#read-qos-playback-buffering-and-device-statistics}

Você pode ler as estatísticas de reprodução, buffering e dispositivo da classe QOSProvider.

A classe `QOSProvider` fornece várias estatísticas, incluindo informações sobre buffering, taxas de bits, taxas de quadros, dados de tempo e assim por diante.

1. Instancie um reprodutor de mídia.
1. Crie um objeto `QOSProvider` e o anexe ao reprodutor de mídia.

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. (Opcional) Leia as estatísticas de reprodução.

   Uma solução para ler as estatísticas de reprodução é ter um temporizador que busca periodicamente os novos valores de QoS do `QOSProvider`. Por exemplo:

   ```js
   var qosTimer = (function () { 
       var ref = null, 
       qosChangeInterval = 500, // in milliseconds 
   
       startTimer = function () { 
           var playbackInformation = qosProvider.playbackInformation; 
        console.log("Frame rate", playbackInformation.frameRate); 
           console.log ("Dropped frames", playbackInformation.droppedFrameCount); 
           console.log ("Bitrate", playbackInformation.bitrate); 
           console.log ("Buffering time", playbackInformation.bufferingTime); 
           console.log ("Buffer length", playbackInformation.bufferLength); 
           console.log ("Buffer time", playbackInformation.bufferTime); 
           console.log ("Empty buffer count", playbackInformation.emptyBufferCount); 
           console.log ("Time to load", playbackInformation.timeToLoad); 
           console.log ("Time to start", playbackInformation.timeToStart); 
           ref = window.setTimeout(startTimer, qosChangeInterval); 
       }; 
   
       return { 
           start: function () { 
               if (ref !== null) { 
                   // don't start another timeout if one already exists. 
                   return; 
               } 
               startTimer(); 
           }, 
   
           stop: function () { 
               window.clearTimeout(ref); 
               ref = null; 
           } 
       };  
   })() 
   
   qosTimer.start(); 
   ```

1. (Opcional) Leia as informações específicas do dispositivo.

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
