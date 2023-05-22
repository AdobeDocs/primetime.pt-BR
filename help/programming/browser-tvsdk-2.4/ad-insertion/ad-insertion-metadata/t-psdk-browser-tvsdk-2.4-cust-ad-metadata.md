---
description: Você pode personalizar e inserir metadados.
title: Personalizar metadados de inserção de anúncios
exl-id: 4881ace6-e97b-448d-8fb4-64e7b69517f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Personalizar metadados de inserção de anúncios{#customize-ad-insertion-metadata}

Você pode personalizar e inserir metadados.

1. Defina um tempo limite nos metadados de publicidade para oportunidades não resolvidas.

   O valor padrão para esse tempo limite é de 20 segundos.
1. Para alterar o valor para 10 segundos, insira o seguinte:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   A variável `timeout` A propriedade é definida no campo `AdvertisingMetadata` e esse tempo limite pode ser definido para qualquer configuração de anúncio personalizada derivada da `AdvertisingMetadata` classe. Por exemplo, se os usuários definirem configurações personalizadas para um resolvedor FreeWheel, poderão definir um tempo limite padrão usando essa configuração.

1. Criar `MediaPlayerItemConfig` com as configurações de publicidade na etapa 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Use esta configuração ao chamar `replaceCurrentResource` em `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
