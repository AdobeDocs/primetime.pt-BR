---
description: Você pode substituir o comportamento padrão de como o TVSDK procura por anúncios ao usar marcadores de anúncios personalizados.
seo-description: Você pode substituir o comportamento padrão de como o TVSDK procura por anúncios ao usar marcadores de anúncios personalizados.
seo-title: Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados
title: Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados
uuid: cf973caf-be29-46ce-bfa4-651e7653f8d4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Controle o comportamento de reprodução para busca em marcadores de anúncio personalizados{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Você pode substituir o comportamento padrão de como o TVSDK procura por anúncios ao usar marcadores de anúncios personalizados.

Por padrão, quando um usuário busca por seções de anúncios passadas ou para dentro que resultam do posicionamento de marcadores de anúncios personalizados, o TVSDK ignora os anúncios. Isso pode ser diferente do comportamento atual de reprodução para quebras de anúncios padrão.

Você pode pedir ao TVSDK para reposicionar o indicador de reprodução no início do anúncio personalizado ignorado mais recentemente quando o usuário buscar mais de um ou mais anúncios personalizados.

1. Configure uma instância de Metadados com a enumeração `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` definida com o valor da string &quot;true&quot; (não como um Booliano `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Crie e configure uma `MediaResource` instância, transmitindo as opções de configuração adicionais para `TimeRangeCollection.toMetadata`. Este método recebe opções de configuração adicionais por meio de outra estrutura de metadados genérica.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```

