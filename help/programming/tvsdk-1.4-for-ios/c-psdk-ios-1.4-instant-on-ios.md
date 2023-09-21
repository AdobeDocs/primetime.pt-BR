---
description: O instantâneo pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou muda de canal, o conteúdo é iniciado mais cedo porque parte do buffering já foi concluído.
title: Instantâneo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Instantâneo{#instant-on}

O instantâneo pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou muda de canal, o conteúdo é iniciado mais cedo porque parte do buffering já foi concluído.

Quando o reprodutor estiver na `PTMediaPlayerStatusReady` status, chamada `prepareToPlay` para pré-carregar e processar parte do conteúdo para reprodução posterior.

>[!TIP]
>
>Se você não chamar `prepareToPlay`, chamando `play` chama automaticamente `prepareToPlay` primeiro. O pré-carregamento e o processamento estão concluídos neste momento.

O TVSDK conclui algumas ou todas as tarefas a seguir para `prepareToPlay`:

* Se a chave de metadados `kSyncCookiesWithAVAsset` for definido, o TVSDK fará uma solicitação ao arquivo M3U8 original para sincronizar cookies.
* Carrega chaves de metadados DRM.
* Cria e prepara algumas estruturas, elementos ou ativos necessários para reproduzir conteúdo.

>[!TIP]
>
>A variável `PTMediaPlayer` e `PTMediaPlayerItem` `prepareToPlay` métodos são iguais. Para evitar a criação de um `PTMediaPlayer` para cada ativo, use o `PTMediaPlayerItem` método.

A ativação instantânea ajuda a iniciar várias instâncias do reprodutor de mídia, ou instâncias do carregador de itens do reprodutor de mídia, simultaneamente em segundo plano e fluxos de vídeo de buffer em todas essas instâncias. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamando `play` no novo canal inicia a reprodução mais cedo.
