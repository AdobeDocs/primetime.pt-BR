---
description: É possível rastrear o uso do vídeo integrando o Browser TVSDK ao Adobe Analytics.
title: Análise de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Análise de vídeo{#video-analytics}

É possível rastrear o uso do vídeo integrando o Browser TVSDK ao Adobe Analytics.

O rastreamento de vídeo no TVSDK do navegador usa o serviço **Adobe Analytics Video Essentials**, que fornece métricas de envolvimento com o vídeo, como exibições de vídeo, conclusões de vídeo, impressões de anúncios, tempo gasto com vídeo etc. Para obter mais informações sobre esse serviço, entre em contato com o representante do Adobe.

O procedimento a seguir resume as etapas para ativar o rastreamento de vídeo no player:

1. Inicialize e/ou configure os seguintes componentes de rastreamento de vídeo:

   * **Biblioteca do AppMeasurement**  - Contém a lógica principal de coleta de dados de baixo nível. É aqui que os dados da pulsação de vídeo são acumulados e enviados pela rede.
   * **Biblioteca do Video Heartbeat**  - Contém a lógica principal de coleta de dados do Video Heartbeat. A biblioteca do Video Heartbeat acessa um subconjunto das APIs da biblioteca AppMeasurement.

      >[!TIP]
      >
      >Seu aplicativo não interage diretamente com o código de pulsação de vídeo. Em vez disso, o aplicativo usa APIs TVSDK do navegador para configurar os recursos de rastreamento de vídeo do player.

   * **Biblioteca VisitorID**  - identifica de forma exclusiva os visitantes da página da Web que hospeda o reprodutor de vídeo.
   >[!IMPORTANT]
   >
   >O recurso integrado de rastreamento de vídeo TVSDK do navegador depende de uma instância do AppMeasurement devidamente configurada. Os elementos de rastreamento presumem que a biblioteca do AppMeasurement já está instanciada e configurada antes de configurar e ativar o rastreamento de vídeo. Os recursos de rastreamento de vídeo TVSDK do navegador dependem da existência de uma instância totalmente funcional e configurada corretamente da biblioteca do AppMeasurement.

1. Configure os relatórios de análise de vídeo no lado do servidor usando as Ferramentas administrativas do Adobe Analytics.