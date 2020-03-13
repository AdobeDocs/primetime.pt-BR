---
description: O Instant-on pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou alterna os canais, o conteúdo é iniciado mais cedo porque alguns dos buffering já foram concluídos.
seo-description: O Instant-on pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou alterna os canais, o conteúdo é iniciado mais cedo porque alguns dos buffering já foram concluídos.
seo-title: Instant-on
title: Instant-on
uuid: 23864919-9045-4223-9e47-464e38ebe5ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Instant-on{#instant-on}

O Instant-on pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou alterna os canais, o conteúdo é iniciado mais cedo porque alguns dos buffering já foram concluídos.

Quando o player estiver com o `PTMediaPlayerStatusReady` status, chame `prepareToPlay` para pré-carregar e processar parte do conteúdo para reprodução posterior.

>[!TIP]
>
>Se você não ligar `prepareToPlay`, chamar `play` automaticamente chama `prepareToPlay` primeiro. O pré-carregamento e o processamento estão concluídos no momento.

O TVSDK conclui algumas ou todas as seguintes tarefas para `prepareToPlay`:

* Se a chave de metadados `kSyncCookiesWithAVAsset` estiver definida, o TVSDK faz uma solicitação para o arquivo M3U8 original para sincronizar os cookies.
* Carrega chaves de metadados DRM.
* Cria e prepara algumas estruturas, elementos ou ativos necessários para reproduzir conteúdo.

>[!TIP]
>
>Os métodos `PTMediaPlayer` e `PTMediaPlayerItem``prepareToPlay` são iguais. Para evitar a criação de uma `PTMediaPlayer` instância separada para cada ativo, use o `PTMediaPlayerItem` método.

O Instant-on ajuda a iniciar várias instâncias do player de mídia, ou instâncias do carregador de itens do player de mídia, simultaneamente em streams de vídeo em segundo plano e buffer em todas essas instâncias. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamar `play` o novo canal inicia a reprodução mais cedo.
