---
description: A Qualidade do serviço (QoS) fornece uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
title: Estatísticas de qualidade dos serviços
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Estatísticas de qualidade do serviço {#quality-of-service-statistics}

A Qualidade do serviço (QoS) fornece uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.

O TVSDK também fornece informações sobre os seguintes recursos baixados:

* Arquivos Playlist/manifest
* Fragmentos de arquivo
* Rastreamento de informações para arquivos

## Rastrear no nível do fragmento usando informações de carregamento {#section_4439D91E8EDC45588EF1D7BE25697350}

Você pode ler informações de qualidade do serviço (QoS) sobre os recursos baixados, como fragmentos e rastreamentos, da classe `LoadInformation`.

1. Implemente e registre o ouvinte do evento `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`.
1. Chame `event.getLoadInformation()` para ler os dados relevantes do parâmetro `event` passado para o retorno de chamada.

   >[!NOTE]
   >
   >Para obter mais informações sobre `LoadInformation`, consulte [3.0 para documentos da API do Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.0/index.html).

## Ler a reprodução do QOS, o buffering e as estatísticas do dispositivo {#section_D21722600F324E67A9F06234D338B243}

Você pode ler as estatísticas de reprodução, buffering e dispositivo da classe `QOSProvider`.

A classe `QOSProvider` fornece várias estatísticas, incluindo informações sobre buffering, taxas de bits, taxas de quadros, dados de tempo e assim por diante. Ele também fornece informações sobre o dispositivo, como fabricante, modelo, sistema operacional, versão do SDK, ID do dispositivo do fabricante e tamanho/densidade da tela.

1. Instancie um reprodutor de mídia.
1. Crie um objeto `QOSProvider` e o anexe ao reprodutor de mídia.

   O construtor `QOSProvider` assume um contexto de reprodutor para que possa recuperar informações específicas do dispositivo.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Leia as estatísticas de reprodução.

   Uma solução para ler as estatísticas de reprodução é ter um temporizador que busca periodicamente os novos valores de QoS do `QOSProvider`.

   Por exemplo:

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation =  
                     _mediaQosProvider.getPlaybackInformation();  
                   setQosItem("Frame rate", (int) playbackInformation.getFrameRate());  
                   setQosItem("Dropped frames", (int) playbackInformation.getDroppedFrameCount()); 
                   setQosItem("Bitrate", (int) playbackInformation.getBitrate()); 
                   setQosItem("Buffering time", (int) playbackInformation.getBufferingTime());  
                   setQosItem("Buffer length", (int) playbackInformation.getBufferLength());  
                   setQosItem("Buffer time", (int) playbackInformation.getBufferTime());  
                   setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount());  
                   setQosItem("Time to load", (int) playbackInformation.getTimeToLoad());  
                   setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); 
                   setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); 
                   setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());   
                   playbackInformation.getPerceivedBandwidth()); 
               } 
           }); 
       }; 
   }; 
   ```

1. (Opcional) Leia as informações específicas do dispositivo.

   ```java
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider(parent.getApplicationContext()). 
                                  getDeviceInformation(); 
   tv = (TextView) view.findViewById(R.id.aboutDeviceModel); 
   tv.setText(parent.getString(R.string.aboutDeviceModel) + " " +  
     deviceInfo.getManufacturer() + " - " + deviceInfo.getModel()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceSoftware); 
   tv.setText(parent.getString(R.string.aboutDeviceSoftware) + " " +  
     deviceInfo.getOS() + ", SDK: " + deviceInfo.getSDK()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceResolutin); 
   String orientation = parent.getResources().getConfiguration().orientation ==  
     Configuration.ORIENTATION_LANDSCAPE ? "landscape" : "portrait"; 
   tv.setText(parent.getString(R.string.aboutDeviceResolution) + " " +  
     deviceInfo.getWidthPixels() + "x" + deviceInfo.getHeightPixels() +  
     " (" + orientation + ")"); 
   ```
