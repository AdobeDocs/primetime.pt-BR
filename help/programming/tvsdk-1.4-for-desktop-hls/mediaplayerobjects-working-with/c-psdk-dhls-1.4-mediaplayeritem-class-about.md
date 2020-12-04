---
description: O objeto MediaPlayer representa o player de mídia. Um MediaPlayerItem representa áudio ou vídeo no player.
seo-description: O objeto MediaPlayer representa o player de mídia. Um MediaPlayerItem representa áudio ou vídeo no player.
seo-title: Sobre a classe MediaPlayerItem
title: Sobre a classe MediaPlayerItem
uuid: 531dd1a6-d72c-4ae3-9c3f-2f1d854245c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Sobre a classe MediaPlayerItem{#about-the-mediaplayeritem-class}

O objeto MediaPlayer representa o player de mídia. Um MediaPlayerItem representa áudio ou vídeo no player.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

Depois que um recurso de mídia é carregado com êxito, o TVSDK cria uma instância da classe `MediaPlayerItem` para fornecer acesso a esse recurso.

O `MediaResource` representa uma solicitação emitida pela camada do aplicativo para a instância `MediaPlayer` para carregar o conteúdo.

O `MediaPlayer` resolve o recurso de mídia, carrega o arquivo manifest associado e analisa o manifesto. Esta é a parte assíncrona do processo de carregamento de recursos. A instância `MediaPlayerItem` é produzida depois que o recurso é resolvido, e essa instância é uma versão resolvida de `MediaResource`. O TVSDK fornece acesso à instância `MediaPlayerItem` recém-criada por meio de `MediaPlayer.currentItem`.

>[!TIP]
>
>É necessário aguardar o carregamento do recurso com êxito antes de acessar o item do player de mídia.

