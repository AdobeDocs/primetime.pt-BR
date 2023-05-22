---
description: Depois que um MediaResource é carregado com êxito, o TVSDK do navegador cria uma ocorrência da classe MediaPlayerItem para fornecer acesso a esse recurso.
title: Sobre a classe MediaPlayerItem
exl-id: 6e47914c-3d46-4aaf-9144-1a00d886e5bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Sobre a classe MediaPlayerItem{#about-the-mediaplayeritem-class}

Depois que um MediaResource é carregado com êxito, o TVSDK do navegador cria uma ocorrência da classe MediaPlayerItem para fornecer acesso a esse recurso.

A variável `MediaResource` representa uma solicitação emitida pela camada do aplicativo para o `MediaPlayer` instância para carregar conteúdo.

A variável `MediaPlayer` resolve o recurso de mídia, carrega o arquivo de manifesto associado e analisa o manifesto. Essa é a parte assíncrona do processo de carregamento de recursos. A variável `MediaPlayerItem` instância é produzida depois que o recurso é resolvido e essa instância é uma versão resolvida de um `MediaResource`. O TVSDK do navegador fornece acesso ao recém-criado `MediaPlayerItem` instância por meio de `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Aguarde até que o recurso seja carregado com êxito antes de acessar o item do reprodutor de mídia.
