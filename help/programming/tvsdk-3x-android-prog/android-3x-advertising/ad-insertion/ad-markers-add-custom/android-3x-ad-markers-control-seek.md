---
description: Você pode substituir o comportamento padrão de como o TVSDK lida com buscas por anúncios ao usar marcadores de anúncios personalizados.
title: Controlar o comportamento da reprodução para buscar nos marcadores de anúncios personalizados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Controlar o comportamento da reprodução para buscar nos marcadores de anúncios personalizados {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Você pode substituir o comportamento padrão de como o TVSDK lida com buscas por anúncios ao usar marcadores de anúncios personalizados.

Por padrão, quando um usuário busca em ou seções de anúncios anteriores que resultam do posicionamento de marcadores de anúncios personalizados, o TVSDK ignora os anúncios. Isso pode ser diferente do comportamento de reprodução atual para ad breaks padrão. É possível definir o TVSDK para reposicionar o indicador de reprodução no início do anúncio personalizado ignorado mais recentemente quando o usuário procura por um ou mais anúncios personalizados.

1. Chame `CustomRangeMetadata.setAdjustSeekPosition` com `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Uso `customRangeMetadata` in `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
