---
description: O TVSDK do navegador prepara objetos TimedMetadata para as tags assinadas sempre que esses objetos são encontrados no arquivo MPD (Media Presentation Description) .
title: Assinar tags de anúncio personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Inscrever-se em tags de anúncio personalizadas{#subscribe-to-custom-ad-tags}

O TVSDK do navegador prepara objetos TimedMetadata para as tags assinadas sempre que esses objetos são encontrados no arquivo MPD (Media Presentation Description) .

Você deve assinar as tags antes do início da reprodução.
Para se inscrever nas tags, defina um vetor que contenha os nomes das tags personalizadas para a propriedade `subscribedTags` . Se também for necessário alterar as tags de anúncio usadas pelo gerador de oportunidade padrão, defina um vetor que contenha os nomes personalizados das tags de anúncio para a propriedade `adTags` .

Para se inscrever em tags personalizadas:

1. Crie uma nova configuração de item do reprodutor de mídia.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Crie um vetor de cadeia de caracteres vazio.

   ```js
   var subscribeTags = [];
   ```

1. Adicione os nomes de tag personalizados a este vetor.

   >[!IMPORTANT]
   >
   >Se você estiver lidando com fluxos HLS, lembre-se de incluir o prefixo `#`.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Atribua o vetor atualizado à propriedade `mediaPlayerItemConfig.subscribeTags`.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Crie um vetor de cadeia de caracteres vazio.

   ```js
   var adTags= [];
   ```

1. Adicione o nome personalizado da tag de anúncio a este vetor.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Atribua o vetor atualizado à propriedade `mediaPlayerItemConfig.adTags`.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Use a configuração de item do reprodutor de mídia ao carregar o fluxo de mídia.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

