---
description: Foram introduzidas novas APIs que instruirão o TVSDK a ignorar o estado de conectividade de rede ao baixar manifestos.
title: Reprodução offline com Android
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Reprodução offline com Android {#offline-playback-with-android}

As seguintes APIs foram introduzidas para instruir o TVSDK a ignorar o estado de conectividade de rede ao baixar manifestos. O estado de conectividade de rede geralmente é usado durante o Adaptive Bitrate Streaming (ABR), para determinar se é necessário tentar um fallback ou esperar a retomada da rede.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Você pode habilitar esta configuração e ignorar a conectividade de rede.

Definir `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` para verdadeiro. O valor padrão de um booleano é false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
