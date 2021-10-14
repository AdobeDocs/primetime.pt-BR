---
title: Inicializar e configurar análises de vídeo
description: Inicializar e configurar análises de vídeo
copied-description: true
exl-id: 26bdc11e-b8f6-414f-a3e9-53bc895d25ce
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Inicializar e configurar análises de vídeo {#initialize-and-configure-video-analytics}

Você pode configurar o player para rastrear e analisar o uso do vídeo.
Antes de ativar o rastreamento de vídeo (pulsações de vídeo), verifique se você tem o seguinte:

* TVSDK 3.0 para Android.
* Informações de configuração/inicialização

   Entre em contato com o representante do Adobe para obter as informações específicas da sua conta de monitoramento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>Importante:  Este nome de arquivo de configuração JSON deve permanecer <span class="filepath"> ADBMobileConfig.json </span>. Não é possível alterar o nome e o caminho deste ficheiro de configuração. O caminho para esse arquivo deve ser <span class="filepath"> &lt;source root&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento do AppMeasurement </td> 
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


   1. Confirme se o arquivo `ADBMobileConfig.json` contém os valores apropriados (fornecidos por Adobe).
   1. Confirme se este arquivo está localizado na pasta `assets/`.

      Essa pasta deve estar localizada na raiz da árvore de origem do aplicativo.

   1. Compile e crie seu aplicativo.
   1. Implante e execute o aplicativo agrupado.

      Para obter mais informações sobre essas configurações de AppMeasurement, consulte [Medição de vídeo no Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).

1. Inicialize e configure os metadados de rastreamento da pulsação de vídeo.

   >[!IMPORTANT]
   >
   >Você pode interromper o midstream do módulo de análise de vídeo e reinicializá-lo novamente, conforme necessário. Antes de reinicializar o módulo, verifique se os metadados de análise de vídeo também são atualizados para os metadados de conteúdo corretos. Para recriar os metadados, repita as duas primeiras etapas abaixo (subetapas **a** e **b**).

   1. Crie uma instância dos metadados do Video Analytics.

      Essa instância contém todas as informações de configuração necessárias para ativar o rastreamento de pulsação de vídeo. Por exemplo:

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. Inicialize o provedor do Video Analytics.

      Depois de criar uma instância do reprodutor de mídia, você deve criar uma instância do provedor do Video Analytics e fornecer o contexto do aplicativo a ela.

      >[!TIP]
      >
      >Sempre crie uma nova instância de provedor para cada sessão de reprodução de conteúdo e remova a referência anterior após desconectar a instância do reprodutor de mídia.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. Defina os metadados do Video Analytics na instância `videoAnalyticsProvider`.

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. Anexe a instância do reprodutor de mídia à instância `videoAnalyticsProvider`:

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Destrua o provedor do Video Analytics.

      Antes de iniciar uma nova sessão de reprodução de conteúdo, destrua a instância anterior do provedor de vídeo. Depois de receber o evento de conclusão de conteúdo (ou notificação), aguarde alguns minutos antes de destruir a instância do provedor de análises de vídeo. A destruição imediata da instância pode interferir na capacidade do provedor do Video Analytics de enviar um ping de &quot;vídeo concluído&quot;.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. Marca manualmente o fluxo Live/Linear como concluído.

      Se você tiver vários episódios em um stream ao vivo, é possível marcar manualmente um episódio como concluído usando a API completa. Isso encerra a sessão de rastreamento de vídeo do episódio atual e você pode iniciar uma nova sessão de rastreamento do próximo episódio.

      >[!TIP]
      >
      >Essa API é opcional e não funciona no rastreamento de vídeo VOD.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
