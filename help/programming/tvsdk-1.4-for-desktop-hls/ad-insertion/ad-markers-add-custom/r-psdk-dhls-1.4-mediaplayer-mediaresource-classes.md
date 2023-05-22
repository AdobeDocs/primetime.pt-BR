---
description: Um MediaResource representa o conteúdo que será carregado pela instância MediaPlayer.
title: Classes MediaPlayer e MediaResource
exl-id: c431c9f9-98a3-402c-b799-450f30f668dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Classes MediaPlayer e MediaResource{#mediaplayer-and-mediaresource-classes}

Um MediaResource representa o conteúdo que será carregado pela instância MediaPlayer.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

A biblioteca do TVSDK fornece um meio simples de carregar e preparar conteúdo para reprodução usando o `replaceCurrentResource` no `MediaPlayer` interface. Este método recebe uma instância do `MediaResource` como único argumento de entrada. A variável `MediaResource` A classe é composta pelas seguintes informações:

* Um URL, que representa o local do conteúdo que está prestes a ser carregado.
* Um tipo, que é o tipo de conteúdo que está prestes a ser carregado.

   É uma cadeia de caracteres que define os tipos de conteúdo que podem ser carregados pelo `MediaPlayer`. Os valores possíveis são HLS e HDS. Cada valor está associado à string que representa as extensões de arquivo normalmente usadas, &quot;m3u8&quot; para HLS e &quot;f4m&quot; para HDS.
* Alguns metadados, que é uma instância do `Metadata` classe.

   Essa estrutura semelhante a um dicionário pode conter informações adicionais sobre o conteúdo que será carregado, como informações sobre o conteúdo alternativo/publicitário que deve ser colocado no conteúdo principal.

Os metadados são o meio pelo qual as informações relacionadas ao conteúdo alternativo são passadas para o TVSDK. A variável `Metadata` define a API para um armazenamento de valor-chave genérico, em que a chave e o valor são strings simples.
