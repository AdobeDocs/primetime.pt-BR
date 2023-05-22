---
description: O objeto MediaPlayer representa o reprodutor de mídia. Um MediaPlayerItem representa o áudio ou o vídeo no player.
title: Sobre a classe MediaPlayerItem
exl-id: ff7011ae-57d7-41e1-98be-5319bdc6f799
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Sobre a classe MediaPlayerItem{#about-the-mediaplayeritem-class}

O objeto MediaPlayer representa o reprodutor de mídia. Um MediaPlayerItem representa o áudio ou o vídeo no player.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

Depois que um recurso de mídia é carregado com êxito, o TVSDK cria uma instância do `MediaPlayerItem` para fornecer acesso a esse recurso.

A variável `MediaResource` representa uma solicitação emitida pela camada do aplicativo para o `MediaPlayer` instância para carregar conteúdo.

A variável `MediaPlayer` resolve o recurso de mídia, carrega o arquivo de manifesto associado e analisa o manifesto. Essa é a parte assíncrona do processo de carregamento de recursos. A variável `MediaPlayerItem` instância é produzida depois que o recurso é resolvido e essa instância é uma versão resolvida de um `MediaResource`. O TVSDK fornece acesso ao recém-criado `MediaPlayerItem` instância por meio de `MediaPlayer.currentItem`.

>[!TIP]
>
>Aguarde até que o recurso seja carregado com êxito antes de acessar o item do reprodutor de mídia.
