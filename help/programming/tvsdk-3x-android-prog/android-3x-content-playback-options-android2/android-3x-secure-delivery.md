---
description: O TVSDK apresenta delivery seguro em HTTPS.
seo-description: O TVSDK apresenta delivery seguro em HTTPS.
seo-title: Delivery seguro em HTTPS
title: Delivery seguro em HTTPS
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Delivery seguro em HTTPS {#secure-delivery-https}

O Adobe Primetime TVSDK fornece suporte para o delivery HTTPS para todas as chamadas originadas do TVSDK, que incluem

* Chamadas de servidor de anúncios do Auditude
* Pedidos CRS
* Chamadas de licença DRM
* Pings do Video Analytics
* Faturamento

Para usar esse recurso, verifique se os servidores configurados para atender às solicitações acima são compatíveis com HTTPS.

Esse novo comportamento não é ativado por padrão. Use o seguinte para ativar o delivery seguro antes de chamar `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
