---
description: Você pode personalizar os metadados de inserção de anúncios.
title: Personalizar metadados de inserção de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Personalizar metadados de inserção de anúncio{#customize-ad-insertion-metadata}

Você pode personalizar os metadados de inserção de anúncios.

1. Defina um tempo limite em metadados de anúncio para oportunidades não resolvidas.

   O valor padrão para esse tempo limite é de 20 segundos.
1. Para alterar o valor para 10 segundos, insira o seguinte:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   A propriedade `timeout` é definida na classe `AdvertisingMetadata` e esse tempo limite pode ser definido para qualquer configuração de anúncio personalizada derivada da classe `AdvertisingMetadata`. Por exemplo, se os usuários definirem configurações personalizadas para um resolvedor do FreeWheel, eles poderão definir um tempo limite padrão usando essa configuração.

1. Crie `MediaPlayerItemConfig` com as configurações de anúncio na etapa 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Use essa configuração ao chamar `replaceCurrentResource` em `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

