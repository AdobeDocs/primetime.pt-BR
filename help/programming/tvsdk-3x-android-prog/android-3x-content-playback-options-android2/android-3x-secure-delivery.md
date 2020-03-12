---
description: O TVSDK apresenta entrega segura em HTTPS.
seo-description: O TVSDK apresenta entrega segura em HTTPS.
seo-title: Entrega segura em HTTPS
title: Entrega segura em HTTPS
translation-type: tm+mt
source-git-commit: 4a2271fc481b37bb0a437091de6efe98fcb348d9

---


# Entrega segura em HTTPS {#secure-delivery-https}

O Adobe Primetime TVSDK fornece suporte para entrega HTTPS para todas as chamadas originadas do TVSDK, que incluem

* Chamadas de servidor de anúncios do Auditude
* Pedidos CRS
* Chamadas de licença DRM
* Pings do Video Analytics
* Faturamento

Para usar esse recurso, verifique se os servidores configurados para atender às solicitações acima são compatíveis com HTTPS.

Esse novo comportamento não é ativado por padrão. Use o seguinte para ativar a entrega segura antes de chamar para `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
