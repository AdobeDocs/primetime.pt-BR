---
description: O Instant-on pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou alterna canais, o conteúdo é iniciado antes, pois algum buffering já foi concluído.
title: Instant-on
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Instant-on {#instant-on}

O Instant-on pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou alterna canais, o conteúdo é iniciado antes, pois algum buffering já foi concluído.

Quando o reprodutor estiver no status `PTMediaPlayerStatusReady` , chame `prepareToPlay` para pré-carregar e processar parte do conteúdo para reprodução posterior.

>[!TIP]
>
>Se você não chamar `prepareToPlay`, chamar `play` automaticamente chama `prepareToPlay` primeiro. O pré-carregamento e o processamento são concluídos no momento.

O TVSDK conclui algumas ou todas as seguintes tarefas para `prepareToPlay`:

* Se a chave de metadados `kSyncCookiesWithAVAsset` estiver definida, o TVSDK fará uma solicitação para o arquivo M3U8 original para sincronizar cookies.
* Carrega chaves de metadados de DRM.
* Cria e prepara algumas estruturas, elementos ou ativos necessários para reproduzir conteúdo.

>[!TIP]
>
>Os métodos `PTMediaPlayer` e `PTMediaPlayerItem` `prepareToPlay` são iguais. Para evitar criar uma instância `PTMediaPlayer` separada para cada ativo, use o método `PTMediaPlayerItem` .

O Instant-on ajuda a iniciar várias instâncias do reprodutor de mídia ou instâncias do carregador de itens do reprodutor de mídia, simultaneamente em fluxos de vídeo em segundo plano e em buffer em todas essas instâncias. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamar `play` no novo canal inicia a reprodução mais cedo.