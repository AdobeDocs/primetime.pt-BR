---
description: Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação do Adobe, use a classe BillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.
title: Configurar métricas de faturamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Configurar métricas de faturamento{#configure-billing-metrics}

Se você usar a configuração padrão, não há mais nada que você precise fazer para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação do Adobe, use a classe BillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.

A maioria dos clientes deve usar a configuração padrão.

>[!IMPORTANT]
>
>A configuração definida permanece em vigor durante a vida útil do reprodutor de mídia. Depois de inicializar o reprodutor de mídia, não é possível alterar a configuração.

Para configurar métricas de faturamento:

* Insira a seguinte amostra de código.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   onde `_player` é uma instância de `AdobePSDK.MediaPlayer` e `_resource` é uma instância de `AdobePSDK.MediaResource`.

