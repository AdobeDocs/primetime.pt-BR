---
description: Você pode configurar o player para rastrear e analisar o uso do vídeo.
seo-description: Você pode configurar o player para rastrear e analisar o uso do vídeo.
seo-title: Inicializar e configurar a análise de vídeo
title: Inicializar e configurar a análise de vídeo
uuid: 4a582b35-ae92-4557-806d-e174fc878cc5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---


# Inicializar e configurar a análise de vídeo {#initialize-and-configure-video-analytics}

Você pode configurar o player para rastrear e analisar o uso do vídeo.

Antes de ativar o rastreamento de vídeo (pulsações de vídeo), verifique se você tem o seguinte:

* Informações de inicialização do TVSDK de configuração/navegador - Entre em contato com seu representante de Adobe para obter informações específicas sobre sua conta de rastreamento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
  <tr>
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento do AppMeasurement </td>
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
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento de visitantes </td>
   <td colname="col2"> O URL do terminal back-end que fornece um identificador exclusivo para o visualizador de vídeo atual. </td>
  </tr>
  <tr>
   <td colname="col1"> Editor </td>
   <td colname="col2"> Esta é a Publisher ID, que é fornecida aos clientes pelo representante do Adobe. <p>Dica:  Essa ID não é apenas uma string com o nome da marca/televisão. </p> </td>
  </tr>
 </tbody>
</table>

Para configurar o rastreamento de vídeo no player:

1. Instanciar e configurar a biblioteca VisitorAPI.

       Lembre-se das seguintes informações:
   
   * A instanciação requer um parâmetro de entrada da ID da organização do Marketing Cloud fornecido pelo Adobe.

      Este é um valor de string.
   * A única opção de configuração para a biblioteca VisitorAPI é o URL do terminal back-end que fornece o identificador exclusivo para o usuário atual.
   * A URL do servidor de rastreamento de visitantes é a mesma do servidor de rastreamento do Analytics.

      Para obter informações sobre como implementar o serviço de ID de Visitante, consulte [Implementação do serviço de ID de Visitante](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html).

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. Instanciar e configurar o componente AppMeasurement.

   A instância do AppMeasurement tem muitas opções de configuração. Para obter mais informações, acesse a documentação do [Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer). As opções no código de amostra a seguir ( `account`, `visitorNamespace` e `trackingServer`) são necessárias e os valores são fornecidos por Adobe.

   >[!IMPORTANT]
   >
   >É necessário garantir que a cadeia de dependência esteja configurada corretamente. A instância do AppMeasurement agregação (depende) o componente da API do Visitante.

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
   >No seu aplicativo, verifique se `appMeasurementObject.visitor` está preenchido antes de iniciar o fluxo de análise de vídeo, ou você pode não obter resultados de rastreamento. Esses resultados são indicados pelas mensagens no seu log. Você pode adicionar uma chamada de rastreamento vazia ( `appMeasurementObject.track`), pesquisar a propriedade `visitor` até que ela seja preenchida e iniciar a análise de vídeo.

3. Inicialize e configure os metadados de rastreamento de pulsação de vídeo.

   >[!IMPORTANT]
   >
   >Você pode interromper o fluxo médio do módulo de análise de vídeo e reinicializá-lo novamente, conforme necessário. Antes de reinicializar o módulo, verifique se os metadados de análise de vídeo também estão atualizados para os metadados de conteúdo corretos. Para recriar os metadados, repita as subetapas 1 e 2.

   1. Crie uma instância dos metadados do Video Analytics.
Esta instância contém todas as informações de configuração necessárias para habilitar o rastreamento de pulsação de vídeo. Por exemplo:

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

   2. Depois de criar uma instância do player de mídia, crie uma instância do rastreador do Video Analytics e forneça uma referência à instância do player de mídia.
Lembre-se do seguinte:

      * Sempre crie uma nova instância do rastreador para cada sessão de reprodução de conteúdo e remova a referência anterior (após desanexar a instância do player de mídia).
      * Os metadados criados na sub-etapa 1 devem ser fornecidos no construtor do Controlador do Video Analytics.

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
   4. Marque manualmente o fluxo ao vivo/linear como concluído.
Se você tiver vários episódios em um fluxo ao vivo, é possível marcar manualmente um episódio como concluído usando a API completa. Isso encerra a sessão de rastreamento de vídeo para o episódio de vídeo atual e você pode start uma nova sessão de rastreamento para o próximo episódio.
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
