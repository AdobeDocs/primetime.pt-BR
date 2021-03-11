---
description: Depois que um MediaResource é carregado com êxito, o Browser TVSDK cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.
title: Sobre a classe MediaPlayerItem
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Sobre a classe MediaPlayerItem{#about-the-mediaplayeritem-class}

Depois que um MediaResource é carregado com êxito, o Browser TVSDK cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.

O `MediaResource` representa uma solicitação emitida pela camada do aplicativo para a instância `MediaPlayer` para carregar conteúdo.

O `MediaPlayer` resolve o recurso de mídia, carrega o arquivo manifest associado e analisa o manifesto. Essa é a parte assíncrona do processo de carregamento de recursos. A instância `MediaPlayerItem` é produzida após o recurso ter sido resolvido, e essa instância é uma versão resolvida de um `MediaResource`. O TVSDK do navegador fornece acesso à instância `MediaPlayerItem` recém-criada por meio de `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Aguarde até que o recurso seja carregado com êxito antes de acessar o item do reprodutor de mídia.

