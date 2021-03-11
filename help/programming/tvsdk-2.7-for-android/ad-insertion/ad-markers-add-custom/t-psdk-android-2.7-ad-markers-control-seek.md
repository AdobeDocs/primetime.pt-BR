---
description: Você pode substituir o comportamento padrão de como o TVSDK lida com anúncios ao usar marcadores de anúncios personalizados.
title: Controlar o comportamento da reprodução para busca em marcadores de anúncios personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Controlar o comportamento da reprodução para busca em marcadores de anúncio personalizados {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Você pode substituir o comportamento padrão de como o TVSDK lida com anúncios ao usar marcadores de anúncios personalizados.

Por padrão, quando um usuário busca seções de anúncios ou seções passadas que resultam do posicionamento de marcadores de anúncios personalizados, o TVSDK ignora os anúncios. Isso pode ser diferente do comportamento de reprodução atual para ad breaks padrão. Você pode definir o TVSDK para reposicionar o indicador de reprodução no início do anúncio personalizado ignorado mais recentemente quando o usuário buscar mais de um ou mais anúncios personalizados.

1. Chame `CustomRangeMetadata.setAdjustSeekPosition` com `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Use `customRangeMetadata` em `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```

