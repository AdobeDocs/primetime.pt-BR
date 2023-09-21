---
description: Um MediaResource representa o conteúdo que será carregado pela instância MediaPlayer.
title: Classes MediaPlayer e MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Classes MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

Um MediaResource representa o conteúdo que será carregado pela instância MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

A biblioteca do TVSDK fornece um meio simples de carregar e preparar conteúdo para reprodução usando o `replaceCurrentItem` na interface do MediaPlayer. Esse método recebe uma ocorrência da classe MediaResource como o único argumento de entrada. A classe MediaResource é composta das seguintes informações:

* Um URL, que representa o local do conteúdo que está prestes a ser carregado.
* Um tipo, que é o tipo de conteúdo que está prestes a ser carregado.

  Esta é uma enumeração simples no `MediaResource` classe que define os tipos de conteúdo que podem ser carregados pelo MediaPlayer. Os valores possíveis são HLS e HDS. Cada valor é associado à string que representa as extensões de arquivo normalmente usadas, `m3u8` para HLS e `f4m` para a HDS.
* Alguns metadados, que é uma instância do `Metadata` classe.

  Essa estrutura semelhante a um dicionário pode conter informações adicionais sobre o conteúdo que será carregado, como informações sobre o conteúdo alternativo/publicitário que deve ser colocado no conteúdo principal.

Os metadados são o meio pelo qual as informações relacionadas ao conteúdo alternativo são passadas para o TVSDK. A variável `Metadata` define a API para um armazenamento de valor-chave genérico, em que a chave e o valor são strings simples.
