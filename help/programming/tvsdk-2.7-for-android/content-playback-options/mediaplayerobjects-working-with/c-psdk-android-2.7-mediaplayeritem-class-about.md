---
description: Após carregar com êxito o objeto MediaResource, o TVSDK cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.
seo-description: Após carregar com êxito o objeto MediaResource, o TVSDK cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.
seo-title: Sobre a classe MediaPlayerItem
title: Sobre a classe MediaPlayerItem
uuid: 2d37f358-d158-481b-81d5-27546e9c2e0e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Sobre a classe MediaPlayerItem {#about-the-mediaplayeritem-class}

O objeto MediaPlayer representa o player de mídia. Um MediaPlayerItem representa áudio ou vídeo no player.

Após carregar com êxito o objeto MediaResource, o TVSDK cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.

O `MediaResource` representa uma solicitação emitida pela camada do aplicativo para a `MediaPlayer` instância para carregar o conteúdo.

O `MediaPlayer` resolve o recurso de mídia, carrega o arquivo manifest associado e analisa o manifesto. Esta é a parte assíncrona do processo de carregamento de recursos. A `MediaPlayerItem` instância é produzida depois que o recurso é resolvido, e essa instância é uma versão resolvida de um `MediaResource`. O TVSDK fornece acesso à `MediaPlayerItem` instância recém-criada por meio `MediaPlayer.CurrentItem`.

>[!TIP]
>
>É necessário aguardar o carregamento do recurso com êxito antes de acessar o item do player de mídia.