---
description: O TVSDK do navegador prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no arquivo MPD (Media Presentation Description).
seo-description: O TVSDK do navegador prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no arquivo MPD (Media Presentation Description).
seo-title: Inscrever-se em tags de publicidade personalizadas
title: Inscrever-se em tags de publicidade personalizadas
uuid: 208f61f4-dc33-4363-aa71-878458740a8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Inscrever-se em tags de publicidade personalizadas{#subscribe-to-custom-ad-tags}

O TVSDK do navegador prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no arquivo MPD (Media Presentation Description).

Você deve assinar as tags antes do início da reprodução.
Para assinar as tags, defina um vetor que contenha os nomes das tags personalizadas para a `subscribedTags` propriedade. Se você também precisar alterar as tags de publicidade usadas pelo gerador de oportunidades padrão, defina um vetor que contenha os nomes de tags de publicidade personalizadas para a `adTags` propriedade.

Para assinar tags personalizadas:

1. Crie uma nova configuração de item de media player.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Crie um vetor de string vazio.

   ```js
   var subscribeTags = [];
   ```

1. Adicione os nomes de tags personalizadas a esse vetor.

   >[!IMPORTANT]
   >
   >Se você estiver lidando com fluxos HLS, lembre-se de incluir o `#` prefixo.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Atribua o vetor atualizado à `mediaPlayerItemConfig.subscribeTags` propriedade.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Crie um vetor de string vazio.

   ```js
   var adTags= [];
   ```

1. Adicione o nome da tag de publicidade personalizada a este vetor.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Atribua o vetor atualizado à `mediaPlayerItemConfig.adTags` propriedade.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Use a configuração de item do media player ao carregar o fluxo de mídia.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

