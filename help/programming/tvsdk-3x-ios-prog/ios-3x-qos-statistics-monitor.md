---
description: A Qualidade de serviço (QoS) oferta uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
seo-description: A Qualidade de serviço (QoS) oferta uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
seo-title: Estatísticas da qualidade dos serviços
title: Estatísticas da qualidade dos serviços
uuid: c08c1031-616a-4776-92e2-1c405467689b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Estatísticas de qualidade do serviço {#quality-of-service-statistics}

A Qualidade de serviço (QoS) oferta uma visualização detalhada sobre o desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.

## Leia as estatísticas de reprodução, buffering e dispositivo do QOS {#section_9996406E2D814FA382B77E3041CB02BC}

Você pode ler as estatísticas de reprodução, buffering e dispositivo da classe `PTQOSProvider`.

A classe `PTQOSProvider` fornece várias estatísticas, incluindo informações sobre buffering, taxas de bits, taxas de quadros, dados de tempo e assim por diante.

Ele também fornece informações sobre o dispositivo, como o modelo, o sistema operacional e a ID do dispositivo do fabricante.

>[!TIP]
>
>Não é possível alterar o tamanho do buffer de reprodução, mas é possível monitorar o status do tamanho do buffer para depuração ou análise. `PTPlaybackInformation` inclui propriedades como  `playbackBufferFull` e  `playbackLikelyToKeepUp`.

1. Instanciar um player de mídia.
1. Crie um objeto `PTQOSProvider` e anexe-o ao player de mídia.

   O construtor `PTQOSProvider` usa um contexto de player para que possa recuperar informações específicas do dispositivo.

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (Opcional) Leia as estatísticas de reprodução.

   Uma solução para ler as estatísticas de reprodução é ter um timer, como `NSTimer`, que busca periodicamente os novos valores de QoS do `PTQOSProvider`. Por exemplo:

   ```
   - (void)printPlaybackInfoLog { 
       PTPlaybackInformation *playbackInfo = qosProvider.playbackInformation;  
       if (playbackInfo) { 
           // For example: 
           NSString *infoLog = [NSString stringWithFormat:@"observedBitrate :  
                                  %f\n",playbackInfo.observedBitrate]; 
           [consoleView logMessage:@"====%@\n\n",infoLog]; 
       } 
   }
   ```

1. (Opcional) Leia as informações específicas do dispositivo.

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```
