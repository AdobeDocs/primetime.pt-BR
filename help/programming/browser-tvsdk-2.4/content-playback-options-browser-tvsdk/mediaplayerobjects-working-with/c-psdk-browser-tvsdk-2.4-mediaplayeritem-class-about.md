---
description: Depois que um MediaResource é carregado com êxito, o TVSDK do navegador cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.
seo-description: Depois que um MediaResource é carregado com êxito, o TVSDK do navegador cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.
seo-title: Sobre a classe MediaPlayerItem
title: Sobre a classe MediaPlayerItem
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Sobre a classe MediaPlayerItem{#about-the-mediaplayeritem-class}

Depois que um MediaResource é carregado com êxito, o TVSDK do navegador cria uma instância da classe MediaPlayerItem para fornecer acesso a esse recurso.

O `MediaResource` representa uma solicitação emitida pela camada do aplicativo para a instância `MediaPlayer` para carregar o conteúdo.

O `MediaPlayer` resolve o recurso de mídia, carrega o arquivo manifest associado e analisa o manifesto. Esta é a parte assíncrona do processo de carregamento de recursos. A instância `MediaPlayerItem` é produzida depois que o recurso é resolvido, e essa instância é uma versão resolvida de `MediaResource`. O TVSDK do navegador fornece acesso à instância `MediaPlayerItem` recém-criada por meio de `MediaPlayer.CurrentItem`.

>[!TIP]
>
>É necessário aguardar o carregamento do recurso com êxito antes de acessar o item do player de mídia.

