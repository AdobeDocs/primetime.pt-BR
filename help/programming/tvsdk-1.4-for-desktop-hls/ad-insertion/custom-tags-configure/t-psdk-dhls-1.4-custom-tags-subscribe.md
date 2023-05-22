---
description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.
title: Inscrever-se em tags personalizadas
exl-id: 7a3021cc-d2ba-4a70-9c1f-59766b848a62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Inscrever-se em tags personalizadas{#subscribe-to-custom-tags}

O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.

Antes de começar a reprodução, você deve assinar as tags.
Para assinar tags, atribua um vetor que contenha os nomes de tag personalizados à `subscribedTags` propriedade. Se você também precisar alterar as tags de anúncio usadas pelo gerador de oportunidades padrão, atribua um vetor que contenha os nomes das tags de anúncio personalizadas à `adTags` propriedade.

Para ser notificado sobre tags personalizadas em manifestos HLS:

1. Defina os nomes de tags de anúncio personalizadas globalmente, atribuindo um vetor que contenha as tags personalizadas a `subscribeTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Você deve incluir o `#` prefixo ao trabalhar com fluxos HLS.

   Por exemplo:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Para alterar globalmente as tags de anúncio usadas pelo gerador de oportunidades padrão, atribua um vetor que contenha os nomes das tags de anúncio personalizadas à `adTags` propriedade no `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Para que todas as configurações globais tenham efeito, substitua o recurso atual.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Para definir os nomes de tag assinados para um fluxo, se necessário:
   1. Criar uma configuração de item do reprodutor de mídia.

      >[!TIP]
      >
      >A maneira mais fácil é criar uma configuração padrão de item do reprodutor de mídia.

   1. Atribuir um vetor que contenha as tags personalizadas a `subscribeTags` in `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Para alterar as tags de anúncio usadas pelo gerador de oportunidades padrão no fluxo especificado, atribua um vetor que contenha os nomes das tags de anúncio personalizadas à `adTags` propriedade no `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Para que as alterações no fluxo tenham efeito, ao carregar o fluxo de mídia, use a configuração de item do reprodutor de mídia.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
