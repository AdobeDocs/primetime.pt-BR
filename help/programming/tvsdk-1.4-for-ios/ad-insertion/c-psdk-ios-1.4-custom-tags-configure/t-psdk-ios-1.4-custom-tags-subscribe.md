---
description: O TVSDK prepara objetos PTTimedMetadata para tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.
title: Inscrever-se em tags personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Inscrever-se em tags personalizadas {#subscribe-to-custom-tags}

O TVSDK prepara objetos PTTimedMetadata para tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.

Antes de começar a reprodução, você deve assinar as tags.
Para ser notificado sobre tags personalizadas em manifestos HLS:

1. Defina os nomes das tags de anúncio personalizadas globalmente, transmitindo uma matriz que contém as tags personalizadas para `setSubscribedTags` in `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Você deve incluir o `#` prefixo ao trabalhar com fluxos HLS.

   Por exemplo:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
