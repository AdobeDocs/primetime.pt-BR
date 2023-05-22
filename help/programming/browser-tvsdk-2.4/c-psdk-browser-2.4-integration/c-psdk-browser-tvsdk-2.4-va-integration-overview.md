---
description: Você pode rastrear o uso de vídeos integrando o TVSDK do navegador ao Adobe Analytics.
title: Análise de vídeo
exl-id: b6fb39a9-6cb8-4498-a9fa-0ea19af52a58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Análise de vídeo{#video-analytics}

Você pode rastrear o uso de vídeos integrando o TVSDK do navegador ao Adobe Analytics.

O rastreamento de vídeo no navegador TVSDK usa o **Adobe Analytics Video Essentials** serviço, que fornece métricas de envolvimento com o vídeo, como exibições, conclusões de vídeo, impressões de anúncios, tempo gasto no vídeo e assim por diante. Para obter mais informações sobre esse serviço, entre em contato com o representante da Adobe.

O procedimento a seguir resume as etapas para ativar o rastreamento de vídeo no seu reprodutor:

1. Inicialize e/ou configure os seguintes componentes de rastreamento de vídeo:

   * **Biblioteca AppMeasurement** - Contém a lógica principal da coleta de dados de baixo nível. É aqui que os dados de heartbeat de vídeo são acumulados e enviados pela rede.
   * **Biblioteca de heartbeat de vídeo** - Contém a lógica principal da coleção de dados de video-heartbeat. A biblioteca de heartbeat de vídeo acessa um subconjunto das APIs da biblioteca do AppMeasurement.

      >[!TIP]
      >
      >O aplicativo não interage diretamente com o código de heartbeat de vídeo. Em vez disso, o aplicativo usa APIs TVSDK do navegador para configurar os recursos de rastreamento de vídeo do player.

   * **Biblioteca VisitorID** - Identifica exclusivamente os visitantes da página da Web que hospeda o reprodutor de vídeo.
   >[!IMPORTANT]
   >
   >O recurso de rastreamento de vídeo integrado TVSDK do navegador depende de uma instância do AppMeasurement configurada corretamente. Os elementos de rastreamento presumem que a biblioteca do AppMeasurement já esteja instanciada e configurada antes de configurar e ativar o rastreamento de vídeo. Os recursos de rastreamento de vídeo do TVSDK do navegador dependem da existência de uma instância totalmente funcional e configurada corretamente da biblioteca do AppMeasurement.

1. Configure relatórios de análise de vídeo no lado do servidor usando as Ferramentas administrativas do Adobe Analytics.
