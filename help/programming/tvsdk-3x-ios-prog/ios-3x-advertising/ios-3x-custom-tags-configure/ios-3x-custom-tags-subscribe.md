---
description: O TVSDK prepara objetos PTTimedMetadata para tags assinantes sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-description: O TVSDK prepara objetos PTTimedMetadata para tags assinantes sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-title: Assinar tags personalizadas
title: Assinar tags personalizadas
uuid: e47076b2-6184-4c20-bae4-ba7ae62cf198
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
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
