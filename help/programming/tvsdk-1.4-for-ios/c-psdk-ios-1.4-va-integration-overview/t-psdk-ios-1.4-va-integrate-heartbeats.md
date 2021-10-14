---
description: Você pode configurar o player para rastrear e analisar o uso do vídeo.
title: Inicializar e configurar análises de vídeo
exl-id: dbb1e0b4-2a9e-4687-952d-4772440c1643
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Inicializar e configurar análises de vídeo{#initialize-and-configure-video-analytics}

Você pode configurar o player para rastrear e analisar o uso do vídeo.

Antes de ativar o rastreamento de vídeo (pulsações de vídeo), verifique se você tem o seguinte:

* TVSDK para iOS
* Informações de configuração/inicialização - Entre em contato com o representante do Adobe para obter as informações específicas da conta de rastreamento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>Importante:  Este nome de arquivo de configuração JSON deve permanecer <span class="codeph"> ADBMobileConfig.json </span>. Não é possível alterar o nome e o caminho deste ficheiro de configuração. O caminho para esse arquivo deve ser <span class="codeph"> &lt;source root&gt;/AdobeMobile </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Ponto de extremidade do servidor  </span> de rastreamento do AppMeasurement </td> 
   <td colname="col2"> O URL do ponto de extremidade da coleção de back-end do Adobe Analytics (antigo SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento do Video Analytics </td> 
   <td colname="col2"> O URL do ponto de extremidade da coleção de back-end da análise de vídeo. É aqui que todas as chamadas de rastreamento de pulsação de vídeo são enviadas. <p>Dica:  O URL do servidor de rastreamento do visitante é o mesmo do servidor de rastreamento do Analytics. Para obter informações sobre como implementar o Serviço de ID de visitante, consulte <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> Implementar o Serviço de ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nome da conta </td> 
   <td colname="col2"> Também conhecida como ID do conjunto de relatórios (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID da organização do Marketing Cloud </td> 
   <td colname="col2"> Um valor da string necessário para instanciar o componente Visitante. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editor </td> 
   <td colname="col2"> Esta é a Publisher ID, fornecida aos clientes pelo representante do Adobe. <p>Dica:  Essa ID não é apenas uma string com o nome da marca/televisão. </p> </td> 
  </tr> 
 </tbody> 
</table>

Para configurar o rastreamento de vídeo no player:

1. Confirme se as opções de tempo de carregamento no arquivo de recurso `ADBMobileConfig.json` estão corretas.

   ```
   { 
       "version" : "1.1", 
       "analytics" : { 
           "rsids" : "adobedevelopment", 
           "server" : "10.131.129.149:3000", 
           "charset" : "UTF-8", 
           "ssl" : false, 
           "offlineEnabled" : false, 
           "lifecycleTimeout" : 5, 
           "batchLimit" : 50, 
           "privacyDefault" : "optedin", 
           "poi" : [] 
       }, 
       "marketingCloud": { 
           "org": "ADOBE PROVIDED VALUE"  
       }, 
       "target" : { 
           "clientCode" : "", 
           "timeout" : 5 
       }, 
       "audienceManager" : { 
           "server" : "" 
       } 
   }
   ```

   Esse arquivo de configuração formatado JSON é fornecido como um recurso com TVSDK. O reprodutor lê esses valores somente no momento do carregamento e os valores permanecem constantes enquanto o aplicativo é executado.

   Para configurar as opções de tempo de carregamento:

   1. Confirme se o arquivo `ADBMobileConfig.json` contém os valores apropriados que são fornecidos por Adobe.
   1. Confirme se este arquivo está localizado na pasta `AdobeMobile`.

      Essa pasta deve estar localizada na raiz da árvore de origem do aplicativo.
   1. Compile e crie seu aplicativo.
   1. Implante e execute o aplicativo agrupado.

      Para obter mais informações sobre essas configurações de AppMeasurement, consulte [Medição de vídeo no Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).
1. Inicialize e configure os metadados de rastreamento da pulsação de vídeo.

   >[!IMPORTANT]
   >
   >Você pode interromper o midstream do módulo de análise de vídeo e reinicializá-lo novamente, conforme necessário. Antes de reinicializar o módulo, verifique se os metadados de análise de vídeo também são atualizados para os metadados de conteúdo corretos. Para recriar os metadados, repita as subetapas 1 e 2.

   1. Crie uma instância dos metadados do Video Analytics.

      Essa instância contém todas as informações de configuração necessárias para ativar o rastreamento de pulsação de vídeo. Por exemplo:

      ```
      - (PTVideoAnalyticsTrackingMetadata *)getVideoAnalyticsTrackingMetadata 
      { 
          PTVideoAnalyticsTrackingMetadata *vaTrackingMetadata =  
            [[[PTVideoAnalyticsTrackingMetadata alloc]  
                 initWithTrackingServer:@"example.com" 
                 publisher:@"sample-publisher"] autorelease]; 
      
          // Set these to NO for production deployment. 
          vaTrackingMetadata.debugLogging = YES;  
          vaTrackingMetadata.quietMode = NO; 
      
          vaTrackingMetadata.channel = @"test-channel"; 
          vaTrackingMetadata.videoName = @"myvideo"; 
          vaTrackingMetadata.videoId = @"myvideoid"; 
          vaTrackingMetadata.playerName = @"PSDK Player"; 
          vaTrackingMetadata.enableChapterTracking = YES; 
          vaTrackingMetadata.useSSL = NO; 
          // use this API to override the default asset length -1 for live streams 
          vaTrackingMetadata.assetDuration = SAMPLE_ASSET_DURATION; 
      
      }
      ```

   1. Adicione os metadados do Video Analytics à instância de metadados global.

      Quando estiver pronto, defina a instância dos metadados globais no recurso de mídia ou no item do reprodutor de mídia:

      ```
      - (PTMetadata *)createMetadata 
      { 
          PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
      
          [metadata setMetadata:[self getVideoAnalyticsTrackingMetadata]  
            forKey:PTVideoAnalyticsTrackingMetadataKey]; 
      
          return metadata; 
      } 
      
      PTMetadata *metadata = [self createMetadata]; 
      
      PTMediaPlayerItem *item =  
        [[[PTMediaPlayerItem alloc] initWithUrl:[[[NSURL alloc]  
          initWithString:@"media-url"] autorelease] 
          mediaId:@"media-id" metadata:metadata] autorelease];
      ```

   1. Inicialize o rastreador do Video Analytics.

      Depois de criar uma instância do reprodutor de mídia, você deve criar uma instância do rastreador do Video Analytics e fornecer uma referência à instância do reprodutor de mídia.

      >[!TIP]
      >
      >Sempre crie uma nova instância do rastreador para cada sessão de reprodução de conteúdo e remova a referência anterior após desconectar a instância do reprodutor de mídia.

      ```
      self.videoAnalyticsTracker =  
        [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
      ```

   1. Destrua o rastreador do Video Analytics.

      Antes de iniciar uma nova sessão de reprodução de conteúdo, destrua a instância anterior do rastreador de vídeo. Depois de receber o evento de conclusão de conteúdo (ou notificação), aguarde alguns minutos antes de destruir a instância do rastreador de vídeo. A destruição imediata da instância pode interferir na capacidade do rastreador do Video Analytics de enviar um ping de conclusão de vídeo.

      ```
      self.videoAnalyticsTracker = nil;
      ```

   1. Marca manualmente o fluxo Live/Linear como concluído.

      Se você tiver vários episódios em um stream ao vivo, é possível marcar manualmente um episódio como concluído usando a API completa. Isso encerra a sessão de rastreamento de vídeo do episódio atual e você pode iniciar uma nova sessão de rastreamento do próximo episódio.

      >[!TIP]
      >
      >Essa API é opcional e não é necessária para o rastreamento de vídeo VOD.

      ```
      if (self.videoAnalyticsTracker) 
      { 
         [self.videoAnalyticsTracker trackVideoComplete];   
      }
      ```
