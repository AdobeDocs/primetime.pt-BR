---
description: Após carregar com êxito o objeto MediaResource, o TVSDK cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.
seo-description: Após carregar com êxito o objeto MediaResource, o TVSDK cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.
seo-title: Sobre a classe MediaPlayerItem
title: Sobre a classe MediaPlayerItem
uuid: fc79c442-2e38-48c4-8ef9-6dce9ad6790a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Sobre a classe MediaPlayerItem {#about-the-mediaplayeritem-class}

O objeto MediaPlayer representa o player de mídia. Um MediaPlayerItem representa áudio ou vídeo no player.

Após carregar com êxito o objeto MediaResource, o TVSDK cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.

O `MediaResource` representa uma solicitação emitida pela camada do aplicativo para a `MediaPlayer` instância para carregar o conteúdo.

O `MediaPlayer` resolve o recurso de mídia, carrega o arquivo manifest associado e analisa o manifesto. Esta é a parte assíncrona do processo de carregamento de recursos. A `MediaPlayerItem` instância é produzida depois que o recurso é resolvido, e essa instância é uma versão resolvida de um `MediaResource`. O TVSDK fornece acesso à `MediaPlayerItem` instância recém-criada por meio `MediaPlayer.CurrentItem`.

>[!TIP]
>
>É necessário aguardar o carregamento do recurso com êxito antes de acessar o item do player de mídia.