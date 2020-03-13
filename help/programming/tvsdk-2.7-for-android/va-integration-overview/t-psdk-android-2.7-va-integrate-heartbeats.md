---
description: nulo
seo-description: nulo
seo-title: Inicializar e configurar a análise de vídeo
title: Inicializar e configurar a análise de vídeo
uuid: 98017a20-4997-42f7-9b03-fd9c4b6ccd92
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Inicializar e configurar a análise de vídeo {#initialize-and-configure-video-analytics}

Você pode configurar o player para rastrear e analisar o uso do vídeo.
Antes de ativar o rastreamento de vídeo (pulsações de vídeo), verifique se você tem o seguinte:

* TVSDK 2.5 para Android.
* Informações de configuração / inicialização

   Entre em contato com seu representante da Adobe para obter informações específicas sobre sua conta de rastreamento de vídeo:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Importante:  Este nome de arquivo de configuração JSON deve permanecer <span class="filepath"> ADBMobileConfig.json </span>. Não é possível alterar o nome e o caminho deste ficheiro de configuração. O caminho para este arquivo deve ser <span class="filepath"> &lt;raiz de origem&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento do AppMeasurement </td> 
   <td colname="col2"> O URL do ponto final da coleção back-end do Adobe Analytics (antigo SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Ponto de extremidade do servidor de rastreamento de análise de vídeo </td> 
   <td colname="col2"> O URL do ponto final da coleção de back-end de análise de vídeo. É aqui que todas as chamadas de rastreamento de pulsação de vídeo são enviadas. <p>Dica:  A URL do servidor de rastreamento de visitantes é a mesma do servidor de rastreamento do Analytics. Para obter informações sobre como implementar o serviço de ID de visitante, consulte <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementar o serviço de ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nome da conta </td> 
   <td colname="col2"> Também conhecido como ID do conjunto de relatórios (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID de empresa da Marketing Cloud </td> 
   <td colname="col2"> Um valor de string necessário para instanciar o componente Visitante. </td> 
  </tr> 
 </tbody> 
</table>

Para configurar o rastreamento de vídeo no player:

1. Confirme se as opções de tempo de carregamento no arquivo de `ADBMobileConfig.json` recurso estão corretas.

       &quot;
     {
     &quot;version&quot; : &quot;1.1&quot;,
     &quot;analítica&quot;: {
     &quot;rsids&quot; : &quot;adobedevelopment&quot;,
     &quot;server&quot; : &quot;10.131.129.149:3000&quot;,
     &quot;charset&quot; : &quot;UTF-8&quot;,
     &quot;ssl&quot; : false,
     &quot;offlineEnabled&quot; : false,
     &quot;lifecycleTimeout&quot; : 5,
     &quot;batchLimit&quot;: 50,
     &quot;privacyDefault&quot; : &quot;optedin&quot;,
     &quot;poi&quot; : []
     },
     &quot;marketingCloud&quot;: {
     &quot;org&quot;: &quot;VALOR FORNECIDO PELA ADOBE&quot;
     },
     &quot;destino&quot;: {
     &quot;clientCode&quot; : &quot;&quot;,
     &quot;timeout&quot; : 5
     },
     &quot;audienceManager&quot;: {
     &quot;server&quot; : &quot;&quot;
     }
     }
     &quot;
     
     Este arquivo de configuração formatado por JSON é fornecido como um recurso com TVSDK. O player lê esses valores somente no tempo de carregamento e os valores permanecem constantes enquanto o aplicativo é executado.
       
     Para configurar as opções de tempo de carregamento:
   
   1. Confirme se o `ADBMobileConfig.json` arquivo contém os valores apropriados (fornecidos pela Adobe).
   1. Confirme se este arquivo está localizado na `assets/` pasta.

      Essa pasta deve estar localizada na raiz da árvore de origem do aplicativo.

   1. Compile e crie seu aplicativo.
   1. Implante e execute o aplicativo fornecido.

      Para obter mais informações sobre essas configurações do AppMeasurement, consulte [Medição de vídeo no Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).

1. Inicialize e configure os metadados de rastreamento de pulsação de vídeo.

   >[!IMPORTANT]
   >
   >Você pode interromper o fluxo médio do módulo de análise de vídeo e reinicializá-lo novamente, conforme necessário. Antes de reinicializar o módulo, verifique se os metadados de análise de vídeo também estão atualizados para os metadados de conteúdo corretos. Para recriar os metadados, repita as duas primeiras etapas abaixo (subetapas **a** e **b**).

   1. Crie uma instância dos metadados do Video Analytics.

      Esta instância contém todas as informações de configuração necessárias para habilitar o rastreamento de pulsação de vídeo. Por exemplo:

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

      Depois de criar uma instância de player de mídia, você deve criar uma instância de provedor do Video Analytics e fornecer o contexto do aplicativo para ela.

      >[!TIP]
      >
      >Sempre crie uma nova instância de provedor para cada sessão de reprodução de conteúdo e remova a referência anterior depois de desanexar a instância do player de mídia.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. Defina os metadados do Video Analytics na `videoAnalyticsProvider` instância.

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. Anexe a instância do player de mídia à `videoAnalyticsProvider` instância:

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Destrua o provedor do Video Analytics.

      Antes de iniciar uma nova sessão de reprodução de conteúdo, destrua a instância anterior do provedor de vídeo. Depois de receber o evento de conclusão de conteúdo (ou notificação), aguarde alguns minutos antes de destruir a instância do provedor de análise de vídeo. A destruição imediata da instância pode interferir na capacidade do provedor do Video Analytics de enviar um ping de &quot;vídeo concluído&quot;.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. Marque manualmente o fluxo ao vivo/linear como concluído.

      Se você tiver vários episódios em um fluxo ao vivo, é possível marcar manualmente um episódio como concluído usando a API completa. Isso encerra a sessão de rastreamento de vídeo para o episódio de vídeo atual e você pode iniciar uma nova sessão de rastreamento para o próximo episódio.

      >[!TIP]
      >
      >Essa API é opcional e não funciona no rastreamento de vídeo VOD.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```

