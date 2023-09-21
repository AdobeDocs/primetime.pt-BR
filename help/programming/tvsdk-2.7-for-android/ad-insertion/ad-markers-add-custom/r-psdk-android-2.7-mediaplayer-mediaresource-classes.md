---
description: Um MediaResource representa o conteúdo que será carregado pela instância MediaPlayer.
title: Classes MediaPlayer e MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Classes MediaPlayer e MediaResource {#mediaplayer-and-mediaresource-classes}

Um MediaResource representa o conteúdo que será carregado pela instância MediaPlayer.

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

O TVSDK fornece o meio de carregar e preparar conteúdo para reprodução usando o `replaceCurrentResource` método em `MediaPlayer`. Este método aceita dois argumentos, uma instância de `MediaPlayerResource` e, opcionalmente, uma instância de `MediaPlayerItemConfig`, que você pode usar para transmitir parâmetros personalizados definidos pelo aplicativo.

* Para obter mais detalhes, consulte mediaplayer-reuse-or-remove.
* Para obter detalhes sobre `MediaPlayerResource`, consulte media-resource-create
