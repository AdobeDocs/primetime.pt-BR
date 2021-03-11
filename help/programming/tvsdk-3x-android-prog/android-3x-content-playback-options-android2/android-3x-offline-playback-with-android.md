---
description: 'Foram introduzidas novas APIs que instruirão o TVSDK a ignorar o estado de conectividade de rede ao baixar manifestos. '
title: Reprodução offline com Android
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# Reprodução offline com Android {#offline-playback-with-android}

As APIs a seguir foram introduzidas e instruirão o TVSDK a ignorar o estado de conectividade de rede ao baixar manifestos. O estado de conectividade de rede geralmente é usado durante o ABR (Adaptive Bitrate Streaming), para determinar se é necessário tentar um fallback ou esperar que a rede seja retomada.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Você pode ativar essa configuração e ignorar a conectividade de rede.

Defina `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` como true. O valor padrão para um booleano é false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
