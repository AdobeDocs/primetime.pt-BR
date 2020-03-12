---
description: Você pode ler as estatísticas de reprodução, buffering e dispositivo da classe QOSProvider.
seo-description: Você pode ler as estatísticas de reprodução, buffering e dispositivo da classe QOSProvider.
seo-title: Leia as estatísticas de reprodução, buffering e dispositivo do QOS
title: Leia as estatísticas de reprodução, buffering e dispositivo do QOS
uuid: 19228a50-3721-4dc1-89b6-97458518e272
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Leia as estatísticas de reprodução, buffering e dispositivo do QOS{#read-qos-playback-buffering-and-device-statistics}

Você pode ler as estatísticas de reprodução, buffering e dispositivo da classe QOSProvider.

A `QOSProvider` classe fornece várias estatísticas, incluindo informações sobre buffering, taxas de bits, taxas de quadros, dados de tempo e assim por diante.

Ele também fornece informações sobre o dispositivo, como fabricante, modelo, sistema operacional, versão do SDK, ID do dispositivo do fabricante e tamanho/densidade da tela.

1. Instanciar um player de mídia.
1. Crie um `QOSProvider` objeto e anexe-o ao player de mídia.

   O `QOSProvider` construtor usa um contexto de player para que possa recuperar informações específicas do dispositivo.

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. (Opcional) Leia as estatísticas de reprodução.

   Uma solução para ler as estatísticas de reprodução é ter um timer, que periodicamente obtém os novos valores de QoS do `QOSProvider`. Por exemplo:

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation = _mediaQosProvider.getPlaybackInformation();  
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
   DeviceInformation deviceInfo =  
     new QOSProvider(parent.getApplicationContext()).getDeviceInformation(); 
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

