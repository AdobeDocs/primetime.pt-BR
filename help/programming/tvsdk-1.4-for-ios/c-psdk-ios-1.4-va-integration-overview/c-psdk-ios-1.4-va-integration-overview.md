---
description: É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.
seo-description: É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.
seo-title: Análise de vídeo
title: Análise de vídeo
uuid: 8f297316-f95e-4896-b489-a2d6b36e6b40
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Integração de análise de vídeo {#video-analytics-integration}

É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.

O rastreamento de vídeo no TVSDK usa o serviço **Adobe Analytics Video Essentials**, que fornece métricas de envolvimento de vídeo, como visualizações de vídeo, conclusões de vídeo, impressões de anúncios, tempo gasto no vídeo e assim por diante. Para obter mais informações sobre este serviço, entre em contato com seu representante de Adobe.

O procedimento a seguir resume as etapas para ativar o rastreamento de vídeo no player:

1. Inicialize e/ou configure os seguintes componentes de rastreamento de vídeo:

   No iOS, esses componentes fazem parte do TVSDK:

   * Arquivo de configuração JSON
   * Objeto de metadados de análise de vídeo
   * Objeto de metadados globais
   * Objeto do rastreador de análise de vídeo

1. Configure o relatórios de análise de vídeo no lado do servidor usando as Ferramentas administrativas do Adobe Analytics.