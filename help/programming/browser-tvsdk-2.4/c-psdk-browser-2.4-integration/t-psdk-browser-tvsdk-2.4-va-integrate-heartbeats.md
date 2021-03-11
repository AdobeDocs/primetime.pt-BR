---
description: Você pode configurar o player para rastrear e analisar o uso do vídeo.
title: Inicializar e configurar análises de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---


# Inicializar e configurar análises de vídeo {#initialize-and-configure-video-analytics}

Você pode configurar o player para rastrear e analisar o uso do vídeo.

Antes de ativar o rastreamento de vídeo (pulsações de vídeo), verifique se você tem o seguinte:

* Informações de inicialização do TVSDK de configuração/navegador - Entre em contato com o representante do Adobe para obter as informações específicas da conta de rastreamento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
  <tr>
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento do AppMeasurement </td>
   <td colname="col2"> O URL do ponto de extremidade da coleção de back-end do Adobe Analytics (antigo SiteCatalyst). </td>
  </tr>
  <tr>
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento do Video Analytics </td>
   <td colname="col2"> O URL do ponto de extremidade da coleção de back-end da análise de vídeo. É aqui que todas as chamadas de rastreamento de pulsação de vídeo são enviadas. <p>Dica:  O URL do servidor de rastreamento do visitante é o mesmo do servidor de rastreamento do Analytics. Para obter informações sobre como implementar o Serviço de ID de visitante, consulte <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementar o Serviço de ID </a>. </p> </td>
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
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento do visitante </td>
   <td colname="col2"> O URL do endpoint de back-end que fornece um identificador exclusivo para o visualizador de vídeo atual. </td>
  </tr>
  <tr>
   <td colname="col1"> Editor </td>
   <td colname="col2"> Esta é a Publisher ID, fornecida aos clientes pelo representante do Adobe. <p>Dica:  Essa ID não é apenas uma string com o nome da marca/televisão. </p> </td>
  </tr>
 </tbody>
</table>

Para configurar o rastreamento de vídeo no player:

1. Exemplifique e configure a biblioteca VisitorAPI .

       Lembre-se das seguintes informações:
   
   * A instanciação requer um parâmetro de entrada de ID da organização do Marketing Cloud fornecido pelo Adobe.

      Este é um valor de string.
   * A única opção de configuração da biblioteca VisitorAPI é o URL do endpoint de back-end que fornece o identificador exclusivo para o usuário atual.
   * O URL do servidor de rastreamento do visitante é o mesmo do servidor de rastreamento do Analytics.

      Para obter informações sobre como implementar o Serviço de ID de visitante, consulte [Implementação do Serviço de ID de visitante](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html).

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. Exemplifique e configure o componente AppMeasurement.

   A instância AppMeasurement tem muitas opções de configuração. Para obter mais informações, acesse a documentação do [Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer). As opções no código de amostra a seguir ( `account`, `visitorNamespace` e `trackingServer`) são necessárias e os valores são fornecidos por Adobe.

   >[!IMPORTANT]
   >
   >Você deve garantir que a cadeia de dependência esteja configurada corretamente. A instância do AppMeasurement agrega (depende) o componente da API do visitante.

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = 'URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER';
   appMeasurement.account = 'ACCOUNT_NAME'; // Also known as RSID
   appMeasurement.pageName = 'Sample Page Name';
   appMeasurement.charSet = "UTF-8";
   appMeasurement.visitorID = "test-vid";
   ```

   >[!IMPORTANT]
   >
   >No seu aplicativo, verifique se `appMeasurementObject.visitor` está preenchido antes de iniciar o fluxo de análise de vídeo, ou talvez você não obtenha resultados de rastreamento. Esses resultados são indicados pelas mensagens no seu log. Você pode adicionar uma chamada de rastreamento vazia ( `appMeasurementObject.track`), pesquisar a propriedade `visitor` até que ela seja preenchida e iniciar a análise de vídeo.

3. Inicialize e configure os metadados de rastreamento da pulsação de vídeo.

   >[!IMPORTANT]
   >
   >Você pode interromper o midstream do módulo de análise de vídeo e reinicializá-lo novamente, conforme necessário. Antes de reinicializar o módulo, verifique se os metadados de análise de vídeo também são atualizados para os metadados de conteúdo corretos. Para recriar os metadados, repita as subetapas 1 e 2.

   1. Crie uma instância dos metadados do Video Analytics.
Essa instância contém todas as informações de configuração necessárias para ativar o rastreamento de pulsação de vídeo. Por exemplo:

      ```js
      function getVideoAnalyticsMetadata() {
          var vaObj = new AdobePSDK.VA.VideoAnalyticsMetadata();
          vaObj.appMeasurement = appMeasurement;
          vaObj.trackingServer = 'hbTrackingServer';
          vaObj.publisher = 'hbPublisher';
          vaObj.channel = 'sample-channel';
          vaObj.playerName = 'TVSDK-HTML';
          vaObj.appVersion = '1.0.0';
          vaObj.videoName = 'hbFriendlyName'; // this will overwrite the ContextData variable a.media.friendlyName
          vaObj.assetDuration = durationInSeconds;
          // use this to override the default asset length of -1 for live streams
          vaObj.debugLogging = false;
          return vaObj;
      }
      ```

   2. Depois de criar uma instância do reprodutor de mídia, crie uma instância do rastreador do Video Analytics e forneça uma referência para a instância do reprodutor de mídia.
Lembre-se do seguinte:

      * Sempre crie uma nova instância do rastreador para cada sessão de reprodução do conteúdo e remova a referência anterior (após desanexar a instância do reprodutor de mídia).
      * Os metadados criados na subetapa 1 devem ser fornecidos no construtor do Video Analytics Tracker.

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. Destrua o rastreador do Video Analytics.
Antes de iniciar uma nova sessão de reprodução de conteúdo, destrua a instância anterior do rastreador de vídeo. Depois de receber o evento de conclusão de conteúdo (ou notificação), aguarde alguns minutos antes de destruir a instância do rastreador de vídeo. A destruição imediata da instância pode interferir na capacidade do rastreador do Video Analytics de enviar um ping de conclusão de vídeo.

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```
   4. Marca manualmente o fluxo Live/Linear como concluído.
Se você tiver vários episódios em um stream ao vivo, é possível marcar manualmente um episódio como concluído usando a API completa. Isso encerra a sessão de rastreamento de vídeo do episódio atual e você pode iniciar uma nova sessão de rastreamento do próximo episódio.
      >[!TIP]
      >
      >Essa API é opcional e não é necessária para o rastreamento de vídeo VOD.

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      } 
      ```
