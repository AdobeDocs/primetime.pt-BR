---
description: É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.
seo-description: É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.
seo-title: Integração de análise de vídeo
title: Integração de análise de vídeo
uuid: 275d2c88-a15c-4645-9234-f29d32fc4a63
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Integração de análise de vídeo {#video-analytics-integration}

É possível rastrear o uso do vídeo integrando o TVSDK ao Adobe Analytics.

O rastreamento de vídeo no TVSDK usa o serviço **Adobe Analytics Video Essentials** , que fornece métricas de envolvimento de vídeo, como exibições de vídeo, conclusões de vídeo, impressões de anúncios, tempo gasto no vídeo e assim por diante. Para obter mais informações sobre esse serviço, entre em contato com seu representante da Adobe.

O procedimento a seguir resume as etapas para ativar o rastreamento de vídeo no player:

1. Inicialize e/ou configure os seguintes componentes de rastreamento de vídeo:

   No iOS, esses componentes fazem parte do TVSDK:

   * Arquivo de configuração JSON
   * Objeto de metadados de análise de vídeo
   * Objeto de metadados globais
   * Objeto do rastreador de análise de vídeo

1. Configure os relatórios de análise de vídeo no lado do servidor usando as Ferramentas administrativas do Adobe Analytics.