---
description: Um MediaResource representa o conteúdo que está prestes a ser carregado pela instância do MediaPlayer.
seo-description: Um MediaResource representa o conteúdo que está prestes a ser carregado pela instância do MediaPlayer.
seo-title: Classes MediaPlayer e MediaResource
title: Classes MediaPlayer e MediaResource
uuid: e198f599-22ca-4ea4-bbbb-e239c79174ae
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Classes MediaPlayer e MediaResource {#mediaplayer-and-mediaresource-classes}

Um MediaResource representa o conteúdo que está prestes a ser carregado pela instância do MediaPlayer.

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

O TVSDK fornece os meios de carregar e preparar o conteúdo para reprodução usando o método `replaceCurrentResource` em `MediaPlayer`. Esse método utiliza dois argumentos, uma instância de `MediaPlayerResource` e, opcionalmente, uma instância de `MediaPlayerItemConfig`, que você pode usar para passar parâmetros personalizados definidos pelo aplicativo.

* Para obter mais detalhes, consulte [Reutilizar ou remover uma instância do MediaPlayer](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayerobjects-working-with/android-3x-mediaplayer-reuse-or-remove.md).
* Para obter detalhes de `MediaPlayerResource`, consulte [Criar um recurso de mídia](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-create.md).