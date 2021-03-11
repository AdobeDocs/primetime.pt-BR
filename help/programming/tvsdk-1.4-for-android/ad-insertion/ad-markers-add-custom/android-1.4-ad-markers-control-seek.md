---
description: Você pode substituir o comportamento padrão de como o TVSDK busca anúncios ao usar marcadores de anúncio personalizados.
title: Controlar o comportamento da reprodução para busca em marcadores de anúncios personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Controlar o comportamento da reprodução para busca em marcadores de anúncio personalizados{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Você pode substituir o comportamento padrão de como o TVSDK busca anúncios ao usar marcadores de anúncio personalizados.

Por padrão, quando um usuário busca seções de anúncios ou seções passadas que resultam do posicionamento de marcadores de anúncios personalizados, o TVSDK ignora os anúncios. Isso pode ser diferente do comportamento de reprodução atual para ad breaks padrão.

Você pode solicitar ao TVSDK que reposicione o indicador de reprodução no início do anúncio personalizado ignorado mais recentemente quando o usuário buscar mais de um ou mais anúncios personalizados.

1. Configure uma instância de Metadados com a enumeração `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` definida com o valor da string &quot;true&quot; (não como um Booliano `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Crie e configure uma instância `MediaResource`, transmitindo as opções de configuração adicionais para `TimeRangeCollection.toMetadata`. Esse método recebe opções de configuração adicionais por meio de outra estrutura de metadados genérica.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```

