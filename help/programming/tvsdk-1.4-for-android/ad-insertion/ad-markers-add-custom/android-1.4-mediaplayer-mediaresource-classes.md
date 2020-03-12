---
description: Um MediaResource representa o conteúdo que está prestes a ser carregado pela instância do MediaPlayer.
seo-description: Um MediaResource representa o conteúdo que está prestes a ser carregado pela instância do MediaPlayer.
seo-title: Classes MediaPlayer e MediaResource
title: Classes MediaPlayer e MediaResource
uuid: 7393c320-7dbb-4580-9425-a735f9d03ef5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Classes MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

Um MediaResource representa o conteúdo que está prestes a ser carregado pela instância do MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

A biblioteca TVSDK fornece um meio simples de carregar e preparar o conteúdo para reprodução usando o `replaceCurrentItem` método na interface do MediaPlayer. Este método recebe uma instância da classe MediaResource como o único argumento de entrada. A classe MediaResource é composta das seguintes informações:

* Um URL, que representa o local do conteúdo que está prestes a ser carregado.
* Um tipo, que é o tipo de conteúdo que está prestes a ser carregado.

   Essa é uma enumeração simples na `MediaResource` classe que define os tipos de conteúdo que podem ser carregados pelo MediaPlayer. Os valores possíveis são HLS e HDS. Cada valor é associado à string que representa as extensões de arquivo normalmente usadas, `m3u8` para HLS e `f4m` para HDS.
* Alguns metadados, que é uma instância da `Metadata` classe.

   Essa estrutura semelhante a um dicionário pode conter informações adicionais sobre o conteúdo que está prestes a ser carregado, como informações sobre o conteúdo alternativo/anúncio que deve ser colocado no conteúdo principal.

Os metadados são o meio através do qual as informações relacionadas ao conteúdo alternativo são passadas para o TVSDK. A `Metadata` interface define a API para um armazenamento de valores chave genérico, onde a chave e o valor são strings simples.
