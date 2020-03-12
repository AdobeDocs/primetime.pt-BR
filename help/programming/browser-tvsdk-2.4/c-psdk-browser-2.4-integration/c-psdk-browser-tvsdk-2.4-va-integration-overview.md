---
description: É possível rastrear o uso do vídeo integrando o TVSDK do navegador ao Adobe Analytics.
seo-description: É possível rastrear o uso do vídeo integrando o TVSDK do navegador ao Adobe Analytics.
seo-title: Análise de vídeo
title: Análise de vídeo
uuid: 6351933b-c0f3-4e3e-ad27-bedc8eecc312
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Análise de vídeo{#video-analytics}

É possível rastrear o uso do vídeo integrando o TVSDK do navegador ao Adobe Analytics.

O rastreamento de vídeo no TVSDK do navegador usa o serviço **Adobe Analytics Video Essentials** , que fornece métricas de envolvimento de vídeo, como exibições de vídeo, conclusões de vídeo, impressões de anúncios, tempo gasto no vídeo e assim por diante. Para obter mais informações sobre esse serviço, entre em contato com seu representante da Adobe.

O procedimento a seguir resume as etapas para ativar o rastreamento de vídeo no player:

1. Inicialize e/ou configure os seguintes componentes de rastreamento de vídeo:

   * **Biblioteca** do AppMeasurement - contém a lógica principal de coleta de dados de nível inferior. É aqui que os dados da pulsação de vídeo são acumulados e enviados pela rede.
   * **Biblioteca** de pulsação de vídeo: contém a lógica principal de coleta de dados da pulsação de vídeo. A biblioteca de pulsação de vídeo acessa um subconjunto das APIs da biblioteca do AppMeasurement.

      >[!TIP]
      >
      >Seu aplicativo não interage diretamente com o código de pulsação de vídeo. Em vez disso, o aplicativo usa as APIs TVSDK do navegador para configurar os recursos de rastreamento de vídeo do player.

   * **Biblioteca** VisitorID - identifica os visitantes da página da Web que hospeda o player de vídeo.
   >[!IMPORTANT]
   >
   >O recurso de rastreamento de vídeo incorporado TVSDK do navegador depende de uma instância do AppMeasurement corretamente configurada. Os elementos de rastreamento presumem que a biblioteca do AppMeasurement já está instanciada e configurada antes de configurar e ativar o rastreamento de vídeo. Os recursos de rastreamento de vídeo TVSDK do navegador dependem da existência de uma instância totalmente funcional e corretamente configurada da biblioteca do AppMeasurement.

1. Configure os relatórios de análise de vídeo no lado do servidor usando as Ferramentas administrativas do Adobe Analytics.