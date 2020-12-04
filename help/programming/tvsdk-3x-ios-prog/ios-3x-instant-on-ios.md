---
description: O Instant-on pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou alterna canais, o conteúdo é start mais cedo porque alguns dos buffering já foram concluídos.
seo-description: O Instant-on pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou alterna canais, o conteúdo é start mais cedo porque alguns dos buffering já foram concluídos.
seo-title: Instant-on
title: Instant-on
uuid: 98a5ef79-51e4-474e-a6e8-ca449c430b5e
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Início instantâneo {#instant-on}

O Instant-on pré-carrega partes da mídia em um ou mais canais. Depois que um usuário seleciona ou alterna canais, o conteúdo é start mais cedo porque alguns dos buffering já foram concluídos.

Quando o player estiver no status `PTMediaPlayerStatusReady`, chame `prepareToPlay` para pré-carregar e processar parte do conteúdo para reprodução posterior.

>[!TIP]
>
>Se você não chamar `prepareToPlay`, chamar `play` automaticamente chama `prepareToPlay` primeiro. O pré-carregamento e o processamento estão concluídos no momento.

O TVSDK completa algumas ou todas as seguintes tarefas para `prepareToPlay`:

* Se a chave de metadados `kSyncCookiesWithAVAsset` estiver definida, o TVSDK faz uma solicitação para o arquivo M3U8 original para sincronizar cookies.
* Carrega chaves de metadados DRM.
* Cria e prepara algumas estruturas, elementos ou ativos necessários para reproduzir conteúdo.

>[!TIP]
>
>Os métodos `PTMediaPlayer` e `PTMediaPlayerItem` `prepareToPlay` são iguais. Para evitar criar uma instância `PTMediaPlayer` separada para cada ativo, use o método `PTMediaPlayerItem`.

O Instant-on ajuda a iniciar várias instâncias do player de mídia, ou instâncias do carregador de itens do player de mídia, simultaneamente em streams de vídeo em segundo plano e buffer em todas essas instâncias. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamar `play` no novo canal start a reprodução mais cedo.