---
description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-description: O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.
seo-title: Assinar tags personalizadas
title: Assinar tags personalizadas
uuid: 43480265-4951-466a-a347-6debfb6935ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Inscrever-se em tags personalizadas{#subscribe-to-custom-tags}

O TVSDK prepara objetos TimedMetadata para tags assinadas sempre que esses objetos forem encontrados no manifesto de conteúdo.

Antes dos start de reprodução, você deve assinar as tags.
Para assinar as tags, atribua um vetor que contenha os nomes de tags personalizados à propriedade `subscribedTags`. Se você também precisar alterar as tags de publicidade usadas pelo gerador de oportunidades padrão, atribua um vetor que contenha os nomes de tags de publicidade personalizadas à propriedade `adTags`.

Para ser notificado sobre tags personalizadas em manifestos HLS:

1. Defina os nomes de tags de publicidade personalizadas globalmente atribuindo um vetor que contenha as tags personalizadas a `subscribeTags` em `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Você deve incluir o prefixo `#` ao trabalhar com fluxos HLS.

   Por exemplo:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Para alterar globalmente as tags de publicidade usadas pelo gerador de oportunidades padrão, atribua um vetor que contenha os nomes de tags de publicidade personalizadas à propriedade `adTags` em `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Para que todas as configurações globais tenham efeito, substitua o recurso atual.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Para definir os nomes das tags assinadas para um fluxo, se necessário:
   1. Crie uma configuração de item de media player.

      >[!TIP]
      >
      >A maneira mais fácil é criar uma configuração padrão de item do player de mídia.

   1. Atribua um vetor que contenha as tags personalizadas a `subscribeTags` em `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Para alterar as tags de publicidade usadas pelo gerador de oportunidades padrão no fluxo especificado, atribua um vetor que contenha os nomes de tags de anúncio personalizadas à propriedade `adTags` em `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Para que as alterações no fluxo tenham efeito, ao carregar o fluxo de mídia, use a configuração de item do player de mídia.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

