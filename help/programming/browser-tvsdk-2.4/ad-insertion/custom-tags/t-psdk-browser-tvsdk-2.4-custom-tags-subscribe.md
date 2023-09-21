---
description: O TVSDK do navegador prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no arquivo Media Presentation Description (MPD).
title: Inscrever-se em tags de anúncio personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Inscrever-se em tags de anúncio personalizadas{#subscribe-to-custom-ad-tags}

O TVSDK do navegador prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no arquivo Media Presentation Description (MPD).

Você deve assinar as tags antes do início da reprodução.
Para se inscrever em tags, defina um vetor que contenha os nomes de tag personalizados como `subscribedTags` propriedade. Se também precisar alterar as tags de anúncio usadas pelo gerador de oportunidades padrão, defina um vetor que contenha os nomes das tags de anúncio personalizadas para o `adTags` propriedade.

Para assinar tags personalizadas:

1. Criar uma nova configuração de item do reprodutor de mídia.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Crie um vetor de cadeia de caracteres vazio.

   ```js
   var subscribeTags = [];
   ```

1. Adicione os nomes de tag personalizados a esse vetor.

   >[!IMPORTANT]
   >
   >Se você estiver lidando com fluxos HLS, lembre-se de incluir os `#` prefixo.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Atribua o vetor atualizado à variável `mediaPlayerItemConfig.subscribeTags` propriedade.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Crie um vetor de cadeia de caracteres vazio.

   ```js
   var adTags= [];
   ```

1. Adicione o nome da tag de anúncio personalizada a esse vetor.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Atribua o vetor atualizado à variável `mediaPlayerItemConfig.adTags` propriedade.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Use a configuração do item do reprodutor de mídia ao carregar o fluxo de mídia.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```
