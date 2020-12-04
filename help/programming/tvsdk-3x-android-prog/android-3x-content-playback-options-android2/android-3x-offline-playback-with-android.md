---
description: 'Foram introduzidas novas APIs que instruirão o TVSDK a ignorar o estado de conectividade da rede ao baixar manifestos. '
seo-description: 'Foram introduzidas novas APIs que instruirão o TVSDK a ignorar o estado de conectividade da rede ao baixar manifestos. '
seo-title: Reprodução off-line com Android
title: Reprodução off-line com Android
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Reprodução offline com Android {#offline-playback-with-android}

As APIs a seguir foram introduzidas e instruirão o TVSDK a ignorar o estado de conectividade da rede ao baixar manifestos. O estado de conectividade de rede é geralmente usado durante o ABR (Adaptive Bitrate streaming), para determinar se é necessário tentar um fallback ou esperar a retomada da rede.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

Você pode ativar essa configuração e ignorar a conectividade da rede.

Defina `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` como verdadeiro. O valor padrão para um booliano é falso.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
