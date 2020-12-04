---
description: Você pode configurar o player para rastrear e analisar o uso do vídeo.
seo-description: Você pode configurar o player para rastrear e analisar o uso do vídeo.
seo-title: Inicializar e configurar a análise de vídeo
title: Inicializar e configurar a análise de vídeo
uuid: d1dc9425-e67c-4e13-aee7-302149352506
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---


# Inicializar e configurar a análise de vídeo {#initialize-and-configure-video-analytics}

Você pode configurar o player para rastrear e analisar o uso do vídeo.

Antes de ativar o rastreamento de vídeo (pulsações de vídeo), verifique se você tem o seguinte:

* TVSDK para iOS
* Informações de configuração/inicialização - Entre em contato com seu representante de Adobe para obter informações específicas sobre sua conta de rastreamento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>Importante:  Este nome de arquivo de configuração JSON deve permanecer <span class="codeph"> ADBMobileConfig.json </span>. Não é possível alterar o nome e o caminho deste ficheiro de configuração. O caminho para esse arquivo deve ser <span class="codeph"> &lt;source root&gt;/AdobeMobile </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Ponto de extremidade do servidor  </span> de rastreamento do AppMeasurement </td> 
   <td colname="col2"> O URL do ponto final da coleção back-end do Adobe Analytics (antigo SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento de análise de vídeo </td> 
   <td colname="col2"> O URL do ponto final da coleção de back-end de análise de vídeo. É aqui que todas as chamadas de rastreamento de pulsação de vídeo são enviadas. <p>Dica:  A URL do servidor de rastreamento de visitantes é a mesma do servidor de rastreamento do Analytics. Para obter informações sobre como implementar o serviço de ID de Visitante, consulte <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementar o serviço de ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nome da conta </td> 
   <td colname="col2"> Também conhecido como ID do conjunto de relatórios (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID da organização do Marketing Cloud </td> 
   <td colname="col2"> Um valor de string necessário para instanciar o componente de Visitante. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editor </td> 
   <td colname="col2"> Esta é a Publisher ID, que é fornecida aos clientes pelo representante do Adobe. <p>Dica:  Essa ID não é apenas uma string com o nome da marca/televisão. </p> </td> 
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

   Este arquivo de configuração formatado JSON é fornecido como um recurso com TVSDK. O player lê esses valores somente no tempo de carregamento e os valores permanecem constantes enquanto o aplicativo é executado.

   Para configurar as opções de tempo de carregamento:

   1. Confirme se o arquivo `ADBMobileConfig.json` contém os valores apropriados fornecidos pelo Adobe.
   1. Confirme se este arquivo está localizado na pasta `AdobeMobile`.

      Essa pasta deve estar localizada na raiz da árvore de origem do aplicativo.
   1. Compile e crie seu aplicativo.
   1. Implante e execute o aplicativo fornecido.

      Para obter mais informações sobre essas configurações do AppMeasurement, consulte [Medição de vídeo no Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).
1. Inicialize e configure os metadados de rastreamento de pulsação de vídeo.

   >[!IMPORTANT]
   >
   >Você pode interromper o fluxo médio do módulo de análise de vídeo e reinicializá-lo novamente, conforme necessário. Antes de reinicializar o módulo, verifique se os metadados de análise de vídeo também estão atualizados para os metadados de conteúdo corretos. Para recriar os metadados, repita as subetapas 1 e 2.

   1. Crie uma instância dos metadados do Video Analytics.

      Esta instância contém todas as informações de configuração necessárias para habilitar o rastreamento de pulsação de vídeo. Por exemplo:

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

      Quando estiver pronto, defina a instância de metadados global no recurso de mídia ou no item do player de mídia:

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

      Depois de criar uma instância do player de mídia, é necessário criar uma instância do rastreador do Video Analytics e fornecer uma referência à instância do player de mídia.

      >[!TIP]
      >
      >Sempre crie uma nova instância do rastreador para cada sessão de reprodução de conteúdo e remova a referência anterior depois de desanexar a instância do player de mídia.

      ```
      self.videoAnalyticsTracker =  
        [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
      ```

   1. Destrua o rastreador do Video Analytics.

      Antes de iniciar uma nova sessão de reprodução de conteúdo, destrua a instância anterior do rastreador de vídeo. Depois de receber o evento de conclusão de conteúdo (ou notificação), aguarde alguns minutos antes de destruir a instância do rastreador de vídeo. A destruição imediata da instância pode interferir na capacidade do rastreador do Video Analytics de enviar um ping de conclusão de vídeo.

      ```
      self.videoAnalyticsTracker = nil;
      ```

   1. Marque manualmente o fluxo ao vivo/linear como concluído.

      Se você tiver vários episódios em um fluxo ao vivo, é possível marcar manualmente um episódio como concluído usando a API completa. Isso encerra a sessão de rastreamento de vídeo para o episódio de vídeo atual e você pode start uma nova sessão de rastreamento para o próximo episódio.

      >[!TIP]
      >
      >Essa API é opcional e não é necessária para o rastreamento de vídeo VOD.

      ```
      if (self.videoAnalyticsTracker) 
      { 
         [self.videoAnalyticsTracker trackVideoComplete];   
      }
      ```
