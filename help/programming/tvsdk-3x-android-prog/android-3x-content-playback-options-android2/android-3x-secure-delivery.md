---
description: O TVSDK apresenta entrega segura por HTTPS.
title: Entrega segura por HTTPS
exl-id: 41e2c925-2145-4dfd-909a-aec57dbae9cd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---

# Entrega segura por HTTPS {#secure-delivery-https}

O Adobe Primetime TVSDK oferece suporte ao delivery HTTPS para todas as chamadas originadas do TVSDK, que incluem

* Chamadas do servidor de publicidade auditadas
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
