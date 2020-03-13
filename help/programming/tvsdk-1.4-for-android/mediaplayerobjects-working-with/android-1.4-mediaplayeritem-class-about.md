---
description: O objeto MediaPlayer representa o player de mídia. Um MediaPlayerItem representa áudio ou vídeo no player.
seo-description: O objeto MediaPlayer representa o player de mídia. Um MediaPlayerItem representa áudio ou vídeo no player.
seo-title: Sobre a classe MediaPlayerItem
title: Sobre a classe MediaPlayerItem
uuid: d7f65edf-4693-4b1e-bae0-46fadce98751
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Sobre a classe MediaPlayerItem{#about-the-mediaplayeritem-class}

O objeto MediaPlayer representa o player de mídia. Um MediaPlayerItem representa áudio ou vídeo no player.

Depois que um recurso de mídia é carregado com êxito, o TVSDK cria uma instância da `MediaPlayerItem` classe para fornecer acesso a esse recurso.

O `MediaResource` representa uma solicitação emitida pela camada do aplicativo para a `MediaPlayer` instância para carregar o conteúdo.

O `MediaPlayer` resolve o recurso de mídia, carrega o arquivo manifest associado e analisa o manifesto. Esta é a parte assíncrona do processo de carregamento de recursos. A `MediaPlayerItem` instância é produzida depois que o recurso é resolvido, e essa instância é uma versão resolvida de um `MediaResource`. O TVSDK fornece acesso à `MediaPlayerItem` instância recém-criada por meio de `MediaPlayer.CurrentItem`

>[!TIP]
>
>É necessário aguardar o carregamento do recurso com êxito antes de acessar o item do player de mídia.

