---
description: Você pode personalizar os metadados de inserção de anúncio.
seo-description: Você pode personalizar os metadados de inserção de anúncio.
seo-title: Personalizar metadados de inserção de anúncio
title: Personalizar metadados de inserção de anúncio
uuid: 047470d3-45bd-48be-82ce-4e9d9fe6ea10
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Personalizar metadados de inserção de anúncio{#customize-ad-insertion-metadata}

Você pode personalizar os metadados de inserção de anúncio.

1. Defina um tempo limite nos metadados de publicidade para oportunidades não resolvidas.

   O valor padrão para esse tempo limite é de 20 segundos.
1. Para alterar o valor para 10 segundos, insira o seguinte:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   A propriedade `timeout` é definida na classe `AdvertisingMetadata`, e esse tempo limite pode ser definido para qualquer configuração de anúncio personalizada derivada da classe `AdvertisingMetadata`. Por exemplo, se os usuários definirem configurações personalizadas para um resolvedor FreeWheel, eles poderão definir um tempo limite padrão usando essa configuração.

1. Crie `MediaPlayerItemConfig` com as configurações de anúncio na etapa 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Use essa configuração ao chamar `replaceCurrentResource` em `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

