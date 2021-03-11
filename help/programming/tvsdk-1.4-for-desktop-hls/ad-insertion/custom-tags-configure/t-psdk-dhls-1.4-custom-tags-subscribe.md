---
description: O TVSDK prepara objetos TimedMetadata para as tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.
title: Assinar tags personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# Assinar tags personalizadas{#subscribe-to-custom-tags}

O TVSDK prepara objetos TimedMetadata para as tags assinadas sempre que esses objetos são encontrados no manifesto de conteúdo.

Antes de a reprodução começar, você deve assinar as tags .
Para se inscrever em tags, atribua um vetor que contenha os nomes de tag personalizados à propriedade `subscribedTags` . Se também for necessário alterar as tags de publicidade usadas pelo gerador de oportunidade padrão, atribua um vetor que contenha os nomes de tag de anúncio personalizados à propriedade `adTags` .

Para ser notificado sobre tags personalizadas em manifestos de HLS:

1. Defina os nomes de tag de anúncio personalizados globalmente, atribuindo um vetor que contenha as tags personalizadas para `subscribeTags` em `MediaPlayerItemConfig`.

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

1. Para alterar globalmente as tags de publicidade usadas pelo gerador de oportunidade padrão, atribua um vetor que contenha os nomes de tag de anúncio personalizados à propriedade `adTags` em `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Para que todas as configurações globais entrem em vigor, substitua o recurso atual.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Para definir os nomes das tags subscritas para um fluxo, se necessário:
   1. Criar uma configuração de item do reprodutor de mídia.

      >[!TIP]
      >
      >A maneira mais fácil é criar uma configuração padrão de item do reprodutor de mídia.

   1. Atribua um vetor que contenha as tags personalizadas a `subscribeTags` em `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Para alterar as tags de anúncio usadas pelo gerador de oportunidade padrão no fluxo especificado, atribua um vetor que contenha os nomes de tag de anúncio personalizados à propriedade `adTags` em `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Para que as alterações no fluxo tenham efeito, ao carregar o fluxo de mídia, use a configuração do item do reprodutor de mídia.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

