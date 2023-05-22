---
description: Se você usar a configuração padrão, nada mais precisará ser feito para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação de Adobe, use a classe BillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.
title: Configurar métricas de cobrança
exl-id: 1eb50822-77a0-4b3a-a84c-b6082bcd1cad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Configurar métricas de cobrança{#configure-billing-metrics}

Se você usar a configuração padrão, nada mais precisará ser feito para habilitar ou configurar o faturamento. Se você obteve parâmetros de configuração diferentes do representante de Ativação de Adobe, use a classe BillingMetricsConfiguration para definir esses parâmetros antes de inicializar o reprodutor de mídia.

A maioria dos clientes deve usar a configuração padrão.

>[!IMPORTANT]
>
>A configuração definida permanece em vigor durante a vida útil do reprodutor de mídia. Após inicializar o reprodutor de mídia, não é possível alterar a configuração.

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
