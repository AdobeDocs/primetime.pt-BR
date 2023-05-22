---
description: É possível substituir o comportamento padrão de busca do TVSDK por anúncios ao usar marcadores de anúncios personalizados.
title: Controlar o comportamento da reprodução para buscar nos marcadores de anúncios personalizados
exl-id: 83faa5a4-4416-499e-8cf2-d016cd9a379d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Controlar o comportamento da reprodução para buscar nos marcadores de anúncios personalizados{#control-playback-behavior-for-seeking-over-custom-ad-markers}

É possível substituir o comportamento padrão de busca do TVSDK por anúncios ao usar marcadores de anúncios personalizados.

Por padrão, quando um usuário busca em ou seções de anúncios anteriores que resultam do posicionamento de marcadores de anúncios personalizados, o TVSDK ignora os anúncios. Isso pode ser diferente do comportamento de reprodução atual para ad breaks padrão.

Você pode instruir o TVSDK a reposicionar o indicador de reprodução no início do anúncio personalizado ignorado mais recentemente quando o usuário buscar por um ou mais anúncios personalizados.

1. Configure uma instância de metadados com o `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` enumeração definida como o valor da cadeia de caracteres &quot;true&quot; (não como Booleano) `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Criar e configurar um `MediaResource` instância, transmitindo as opções de configuração adicionais para `TimeRangeCollection.toMetadata`. Esse método recebe opções de configuração adicionais por meio de outra estrutura de metadados genérica.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```
