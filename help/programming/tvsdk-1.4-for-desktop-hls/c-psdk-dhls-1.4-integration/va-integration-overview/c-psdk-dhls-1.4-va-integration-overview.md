---
description: É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.
seo-description: É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.
seo-title: Análise de vídeo
title: Análise de vídeo
uuid: c3cb0574-1117-409c-8aa7-641363d8d85f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Análise de vídeo{#video-analytics}

É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.

O rastreamento de vídeo no TVSDK usa o serviço **Adobe Analytics Video Essentials** , que fornece métricas de envolvimento de vídeo, como exibições de vídeo, conclusões de vídeo, impressões de anúncios, tempo gasto no vídeo e assim por diante. Para obter mais informações sobre esse serviço, entre em contato com seu representante da Adobe.

O procedimento a seguir resume as etapas para ativar o rastreamento de vídeo no player:

1. Inicialize e/ou configure os seguintes componentes de rastreamento de vídeo:

   * **Biblioteca** do AppMeasurement - contém a lógica principal de coleta de dados de nível inferior. É aqui que os dados da pulsação de vídeo são acumulados e enviados pela rede.
   * **Biblioteca** de pulsação de vídeo: contém a lógica principal de coleta de dados da pulsação de vídeo. A biblioteca de pulsação de vídeo acessa um subconjunto das APIs da `AppMeasurement` biblioteca.

      >[!TIP]
      >
      >Seu aplicativo não interage diretamente com o código de pulsação de vídeo. Em vez disso, o aplicativo usa APIs TVSDK para configurar os recursos de rastreamento de vídeo do player.

   * **Biblioteca** VisitorID - identifica os visitantes da página da Web que hospeda o player de vídeo.
   >[!IMPORTANT]
   >
   >O recurso integrado de rastreamento de vídeo TVSDK depende de uma `AppMeasurement` instância configurada corretamente. Os elementos de rastreamento presumem que a `AppMeasurement` biblioteca já está instanciada e configurada antes de configurar e ativar o rastreamento de vídeo. Os recursos de rastreamento de vídeo TVSDK dependem da existência de uma instância totalmente funcional e configurada corretamente da `AppMeasurement` biblioteca.

1. Configure os relatórios de análise de vídeo no lado do servidor usando as Ferramentas administrativas do Adobe Analytics.

