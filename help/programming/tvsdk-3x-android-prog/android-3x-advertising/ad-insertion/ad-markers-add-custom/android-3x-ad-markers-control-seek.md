---
description: Você pode substituir o comportamento padrão de como o TVSDK trata as buscas de anúncios ao usar marcadores de anúncios personalizados.
seo-description: Você pode substituir o comportamento padrão de como o TVSDK trata as buscas de anúncios ao usar marcadores de anúncios personalizados.
seo-title: Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados
title: Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados
uuid: ec95a22f-0143-4c80-826f-d6b40e77cf26
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Você pode substituir o comportamento padrão de como o TVSDK trata as buscas de anúncios ao usar marcadores de anúncios personalizados.

Por padrão, quando um usuário busca por seções de anúncios passadas ou para dentro que resultam do posicionamento de marcadores de anúncios personalizados, o TVSDK ignora os anúncios. Isso pode ser diferente do comportamento atual de reprodução para quebras de anúncios padrão. Você pode definir o TVSDK para reposicionar o indicador de reprodução no início do anúncio personalizado ignorado mais recentemente quando o usuário busca mais de um ou mais anúncios personalizados.

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
