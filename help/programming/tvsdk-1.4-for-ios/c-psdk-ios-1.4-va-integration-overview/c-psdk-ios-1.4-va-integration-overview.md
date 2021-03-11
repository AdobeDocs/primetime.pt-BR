---
description: É possível rastrear o uso do vídeo integrando o TVSDK com o Adobe Analytics.
title: Análise de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Integração do Video Analytics {#video-analytics-integration}

É possível rastrear o uso do vídeo integrando o TVSDK com o Adobe Analytics.

O rastreamento de vídeo no TVSDK usa o serviço **Adobe Analytics Video Essentials**, que fornece métricas de envolvimento com o vídeo, como exibições de vídeo, conclusões de vídeo, impressões de anúncios, tempo gasto com vídeo etc. Para obter mais informações sobre esse serviço, entre em contato com o representante do Adobe.

O procedimento a seguir resume as etapas para ativar o rastreamento de vídeo no player:

1. Inicialize e/ou configure os seguintes componentes de rastreamento de vídeo:

   No iOS, esses componentes fazem parte do TVSDK:

   * Arquivo de configuração JSON
   * Objeto de metadados do Video Analytics
   * Objeto de metadados globais
   * Objeto do rastreador do Video Analytics

1. Configure os relatórios de análise de vídeo no lado do servidor usando as Ferramentas administrativas do Adobe Analytics.