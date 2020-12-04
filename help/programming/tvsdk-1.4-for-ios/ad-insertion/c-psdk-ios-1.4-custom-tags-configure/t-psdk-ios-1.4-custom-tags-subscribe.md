---
description: O TVSDK prepara objetos PTTimedMetadata para tags assinantes sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-description: O TVSDK prepara objetos PTTimedMetadata para tags assinantes sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-title: Assinar tags personalizadas
title: Assinar tags personalizadas
uuid: de66d3db-46d1-485f-9d3a-6e28495bfb13
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

---


# Assine tags personalizadas {#subscribe-to-custom-tags}

O TVSDK prepara objetos PTTimedMetadata para tags assinantes sempre que esses objetos forem encontrados no manifesto de conteúdo.

Antes dos start de reprodução, você deve assinar as tags.
Para ser notificado sobre tags personalizadas em manifestos HLS:

1. Defina os nomes de tags de publicidade personalizadas globalmente transmitindo uma matriz que contenha as tags personalizadas para `setSubscribedTags` em `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Você deve incluir o prefixo `#` ao trabalhar com fluxos HLS.

   Por exemplo:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

