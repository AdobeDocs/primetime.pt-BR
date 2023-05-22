---
description: A Qualidade do serviço (QoS) oferece uma visualização detalhada do desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.
title: Estatísticas de qualidade do serviço
exl-id: 1e9f32fb-3faf-4646-8af1-0c1cc441cb42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Estatísticas de qualidade do serviço {#quality-of-service-statistics}

A Qualidade do serviço (QoS) oferece uma visualização detalhada do desempenho do mecanismo de vídeo. O TVSDK fornece estatísticas detalhadas sobre reprodução, buffering e dispositivos.

## Ler estatísticas de reprodução, buffering e dispositivo de QOS {#section_9996406E2D814FA382B77E3041CB02BC}

Você pode ler as estatísticas de reprodução, buffering e dispositivo no `PTQOSProvider` classe.

A variável `PTQOSProvider` A classe fornece várias estatísticas, incluindo informações sobre buffering, taxas de bits, taxas de quadros, dados de tempo, etc.

Ela também fornece informações sobre o dispositivo, como o modelo, o sistema operacional e a ID do dispositivo do fabricante.

>[!TIP]
>
>Você não pode alterar o tamanho do buffer de reprodução, mas pode monitorar o status do tamanho do buffer para depuração ou análise. `PTPlaybackInformation` inclui propriedades como `playbackBufferFull` e `playbackLikelyToKeepUp`.

1. Instanciar um reprodutor de mídia.
1. Criar um `PTQOSProvider` e anexe-o ao reprodutor de mídia.

   A variável `PTQOSProvider` O construtor usa um contexto do player para recuperar informações específicas do dispositivo.

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (Opcional) Leia as estatísticas de reprodução.

   Uma solução para ler as estatísticas de reprodução é ter um cronômetro, como um `NSTimer`, que busca periodicamente os novos valores de QoS no `PTQOSProvider`. Por exemplo:

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
