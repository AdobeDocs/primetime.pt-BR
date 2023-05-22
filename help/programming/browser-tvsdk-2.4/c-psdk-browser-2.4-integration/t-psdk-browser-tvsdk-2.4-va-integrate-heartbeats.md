---
description: Você pode configurar o player para rastrear e analisar o uso do vídeo.
title: Inicializar e configurar a análise de vídeo
exl-id: e0bf461b-a431-4fba-bd3d-c38be307a92f
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Inicializar e configurar a análise de vídeo {#initialize-and-configure-video-analytics}

Você pode configurar o player para rastrear e analisar o uso do vídeo.

Antes de ativar o rastreamento de vídeo (pulsações de vídeo), verifique se você tem o seguinte:

* Informações de inicialização do TVSDK de configuração/navegador - entre em contato com o representante da Adobe para obter informações específicas da conta de rastreamento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
  <tr>
   <td colname="col1"> Ponto de acesso do servidor de rastreamento do AppMeasurement </td>
   <td colname="col2"> O URL do endpoint da coleção de back-end do Adobe Analytics (antigo SiteCatalyst). </td>
  </tr>
  <tr>
   <td colname="col1"> Ponto de acesso do servidor de rastreamento de análise de vídeo </td>
   <td colname="col2"> A URL do ponto de extremidade da coleção de back-end da análise de vídeo. Aqui, todas as chamadas de rastreamento de heartbeat de vídeo são enviadas. <p>Dica: o URL do servidor de rastreamento do visitante é o mesmo URL do servidor de rastreamento do Analytics. Para obter informações sobre como implementar o Serviço de ID de visitante, consulte <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> Implementar o serviço de ID </a>. </p> </td>
  </tr>
  <tr>
   <td colname="col1"> Nome da conta </td>
   <td colname="col2"> Também conhecida como ID do conjunto de relatórios (RSID). </td>
  </tr>
  <tr>
   <td colname="col1"> ID da organização do Marketing Cloud </td>
   <td colname="col2"> Um valor de string necessário para instanciar o componente Visitante. </td>
  </tr>
  <tr>
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento do visitante </td>
   <td colname="col2"> A URL do ponto de extremidade back-end que fornece um identificador exclusivo para o visualizador de vídeo atual. </td>
  </tr>
  <tr>
   <td colname="col1"> Editor </td>
   <td colname="col2"> Essa é a ID do editor, fornecida aos clientes pelo representante da Adobe. <p>Dica: essa ID não é apenas uma sequência de caracteres com o nome da marca/televisão. </p> </td>
  </tr>
 </tbody>
</table>

Para configurar o rastreamento de vídeo no seu reprodutor:

1. Instancie e configure a biblioteca da API de visitante.

       Lembre-se das seguintes informações:
   
   * A instanciação requer um parâmetro de entrada de ID de organização de Marketing Cloud fornecido por Adobe.

      Este é um valor de sequência de caracteres.
   * A única opção de configuração para a biblioteca VisitorAPI é o URL do ponto de extremidade de back-end que fornece o identificador exclusivo para o usuário atual.
   * O URL do servidor de rastreamento do visitante é o mesmo URL do servidor de rastreamento de análise.

      Para obter informações sobre como implementar o Serviço de ID de visitante, consulte [Implementação do serviço de ID de visitante](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en).

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. Instancie e configure o componente AppMeasurement.

   A instância do AppMeasurement tem muitas opções de configuração. Para obter mais informações, acesse o [Desenvolvedor do Adobe Analytics](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) documentação. As opções no seguinte código de amostra ( `account`, `visitorNamespace`, e `trackingServer`) são obrigatórios e os valores são fornecidos por Adobe.

   >[!IMPORTANT]
   >
   >Você deve garantir que a cadeia de dependência esteja configurada corretamente. A instância do AppMeasurement agrega (depende) do componente da API do visitante.

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
   >No aplicativo, verifique se `appMeasurementObject.visitor` é preenchido antes de iniciar o fluxo de análise de vídeo, ou talvez você não obtenha os resultados de rastreamento. Esses resultados são indicados pelas mensagens no log. Você pode adicionar uma chamada de rastreamento vazia ( `appMeasurementObject.track`), pesquise o `visitor` propriedade até que seja preenchida, e inicie a análise de vídeo.

3. Inicialize e configure os metadados de rastreamento de pulsação de vídeo.

   >[!IMPORTANT]
   >
   >Você pode parar o módulo de análise de vídeo midstream e reinicializá-lo novamente, conforme necessário. Antes de reinicializar o módulo, verifique se os metadados de análise de vídeo também estão atualizados para os metadados de conteúdo corretos. Para recriar os metadados, repita as subetapas 1 e 2.

   1. Crie uma instância dos metadados da Análise de vídeo.
Essa instância contém todas as informações de configuração necessárias para ativar o rastreamento de video heartbeat. Por exemplo:

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

   2. Depois de criar uma instância do reprodutor de mídia, crie uma instância do rastreador do Video Analytics e forneça uma referência à instância do reprodutor de mídia.
Lembre-se do seguinte:

      * Sempre crie uma nova instância do rastreador para cada sessão de reprodução de conteúdo e remova a referência anterior (após desanexar a instância do reprodutor de mídia).
      * Os metadados criados na subetapa 1 devem ser fornecidos no construtor do Video Analytics Tracker.

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. Destruir o rastreador do Video Analytics.
Antes de começar uma nova sessão de reprodução de conteúdo, destrua a instância anterior do rastreador de vídeo. Após receber o evento de conclusão de conteúdo (ou notificação), aguarde alguns minutos antes de destruir a instância do rastreador de vídeo. Destruir a instância imediatamente pode interferir na capacidade do rastreador do Video Analytics de enviar um ping de conclusão de vídeo.

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```

   4. Marca manualmente o fluxo Live/Linear como concluído.
Se você tiver vários episódios em um stream ao vivo, poderá marcar manualmente um episódio como concluído usando a API completa. Isso encerra a sessão de rastreamento de vídeo do episódio de vídeo atual, e você pode iniciar uma nova sessão de rastreamento para o próximo episódio.
      >[!TIP]
      >
      >Essa API é opcional e não é necessária para o rastreamento de vídeo de VOD.

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      }
      ```
