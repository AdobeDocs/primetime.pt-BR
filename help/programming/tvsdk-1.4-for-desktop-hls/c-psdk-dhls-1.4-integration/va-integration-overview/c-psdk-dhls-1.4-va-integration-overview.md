---
description: Você pode rastrear o uso de vídeos integrando o TVSDK ao Adobe Analytics.
title: Análise de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Análise de vídeo{#video-analytics}

Você pode rastrear o uso de vídeos integrando o TVSDK ao Adobe Analytics.

O rastreamento de vídeo no TVSDK usa o **Adobe Analytics Video Essentials** serviço, que fornece métricas de envolvimento com o vídeo, como exibições, conclusões de vídeo, impressões de anúncios, tempo gasto no vídeo e assim por diante. Para obter mais informações sobre esse serviço, entre em contato com o representante da Adobe.

O procedimento a seguir resume as etapas para ativar o rastreamento de vídeo no seu reprodutor:

1. Inicialize e/ou configure os seguintes componentes de rastreamento de vídeo:

   * **biblioteca do AppMeasurement** - Contém a lógica principal da coleta de dados de baixo nível. É aqui que os dados de heartbeat de vídeo são acumulados e enviados pela rede.
   * **Biblioteca de heartbeat de vídeo** - Contém a lógica principal da coleção de dados de video-heartbeat. A biblioteca de heartbeat de vídeo acessa um subconjunto da variável `AppMeasurement` APIs de biblioteca.

     >[!TIP]
     >
     >O aplicativo não interage diretamente com o código de heartbeat de vídeo. Em vez disso, o aplicativo usa APIs TVSDK para configurar os recursos de rastreamento de vídeo do player.

   * **Biblioteca VisitorID** - Identifica exclusivamente os visitantes da página da Web que hospeda o reprodutor de vídeo.

   >[!IMPORTANT]
   >
   >O recurso de rastreamento de vídeo integrado do TVSDK depende de uma configuração correta `AppMeasurement` instância. Os elementos de rastreamento presumem que a variável `AppMeasurement` A biblioteca do já está instanciada e configurada antes de configurar e ativar o rastreamento de vídeo. Os recursos de rastreamento de vídeo do TVSDK dependem da existência de uma instância totalmente funcional e configurada corretamente do `AppMeasurement` biblioteca.

1. Configure relatórios de análise de vídeo no lado do servidor usando as Ferramentas administrativas do Adobe Analytics.
