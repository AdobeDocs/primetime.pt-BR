---
description: Um MediaResource representa o conteúdo que está prestes a ser carregado pela instância MediaPlayer.
title: Classes MediaPlayer e MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Classes MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

Um MediaResource representa o conteúdo que está prestes a ser carregado pela instância MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

A biblioteca TVSDK fornece um meio simples de carregar e preparar o conteúdo para reprodução usando o método `replaceCurrentItem` na interface do MediaPlayer. Esse método recebe uma instância da classe MediaResource como o único argumento de entrada. A classe MediaResource é composta das seguintes informações:

* Um URL, que representa o local do conteúdo que está prestes a ser carregado.
* Um tipo , que é o tipo de conteúdo que está prestes a ser carregado.

   Essa é uma enumeração simples na classe `MediaResource` que define os tipos de conteúdo que podem ser carregados pelo MediaPlayer. Os valores possíveis são HLS e HDS. Cada valor é associado à string que representa as extensões de arquivo normalmente usadas, `m3u8` para HLS e `f4m` para HDS.
* Alguns metadados, que é uma instância da classe `Metadata` .

   Essa estrutura semelhante a um dicionário pode conter informações adicionais sobre o conteúdo que está prestes a ser carregado, como informações sobre o conteúdo alternativo/anúncio que deve ser colocado no conteúdo principal.

Os metadados são o meio pelo qual as informações relacionadas ao conteúdo alternativo são passadas para o TVSDK. A interface `Metadata` define a API de um armazenamento de valor de chave genérico, onde a chave e o valor são strings simples.
