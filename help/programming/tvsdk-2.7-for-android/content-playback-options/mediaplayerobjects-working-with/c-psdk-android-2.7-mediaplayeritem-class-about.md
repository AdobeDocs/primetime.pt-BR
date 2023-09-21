---
description: Após carregar o objeto MediaResource com êxito, o TVSDK cria uma ocorrência da classe MediaPlayerItem para fornecer acesso a esse recurso.
title: Sobre a classe MediaPlayerItem
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Sobre a classe MediaPlayerItem {#about-the-mediaplayeritem-class}

O objeto MediaPlayer representa o reprodutor de mídia. Um MediaPlayerItem representa o áudio ou o vídeo no player.

Após carregar o objeto MediaResource com êxito, o TVSDK cria uma ocorrência da classe MediaPlayerItem para fornecer acesso a esse recurso.

A variável `MediaResource` representa uma solicitação emitida pela camada do aplicativo para o `MediaPlayer` instância para carregar conteúdo.

A variável `MediaPlayer` resolve o recurso de mídia, carrega o arquivo de manifesto associado e analisa o manifesto. Essa é a parte assíncrona do processo de carregamento de recursos. A variável `MediaPlayerItem` instância é produzida depois que o recurso é resolvido e essa instância é uma versão resolvida de um `MediaResource`. O TVSDK fornece acesso ao recém-criado `MediaPlayerItem` instância por meio de `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Aguarde até que o recurso seja carregado com êxito antes de acessar o item do reprodutor de mídia.
