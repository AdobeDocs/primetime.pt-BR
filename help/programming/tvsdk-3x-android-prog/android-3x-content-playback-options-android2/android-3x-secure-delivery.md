---
description: O TVSDK apresenta entrega segura por HTTPS.
title: Entrega segura por HTTPS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# Entrega segura por HTTPS {#secure-delivery-https}

O Adobe Primetime TVSDK oferece suporte ao delivery HTTPS para todas as chamadas originadas do TVSDK, que incluem

* Chamadas de servidor Auditude Ad
* Solicitações CRS
* Chamadas de licença DRM
* Pings de análise de vídeo
* Pings de Cobrança

Para usar esse recurso, verifique se os servidores configurados para atender às solicitações acima são compatíveis com HTTPS.

Esse novo comportamento não é ativado por padrão. Use o seguinte para habilitar a entrega segura antes de chamar `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
