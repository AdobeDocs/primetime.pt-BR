---
description: O TVSDK apresenta entrega segura por HTTPS.
title: Entrega segura por HTTPS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# Entrega segura por HTTPS {#secure-delivery-https}

O Adobe Primetime TVSDK fornece suporte para entrega HTTPS para todas as chamadas originadas do TVSDK, que incluem

* Chamadas de servidor de anúncios do Auditude
* Solicitações de CRS
* Chamadas de licença de DRM
* Pings do Video Analytics
* Pings de Faturamento

Para usar esse recurso, verifique se os servidores configurados para atender às solicitações acima são compatíveis com HTTPS.

Esse novo comportamento não é habilitado por padrão. Use o seguinte para ativar a entrega segura antes de chamar `MediaPlayer.replaceCurrentResource()`

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(context);
NetworkConfiguration netConfig  = new NetworkConfiguration();
netConfig.setForceHTTPS(true);
config.setNetworkConfiguration(netConfig);
```
