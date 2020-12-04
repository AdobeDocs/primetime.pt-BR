---
description: Essas classes descrevem eventos que o TVSDK envia para o player de mídia em resposta a várias atividades.
seo-description: Essas classes descrevem eventos que o TVSDK envia para o player de mídia em resposta a várias atividades.
seo-title: Classes de eventos
title: Classes de eventos
uuid: 5e63d43c-6112-4958-b8cd-ccf123affd08
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Classes de eventos {#events-classes}

Essas classes descrevem eventos que o TVSDK envia para o player de mídia em resposta a várias atividades.

Pacote: [com.adobe.mediacore.eventos](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| Nome | Significado |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | Classe. Uma pausa de anúncio iniciada ou concluída. |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | Classe. O usuário clicou em um anúncio. |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | Classe. O jogador tocou um anúncio. |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | Classe. O player iniciou ou parou o buffering. |
| [CustomAdEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/CustomAdEvent.html) | Classe. O player exibe o status de carregamento de anúncio personalizado e pode ignorar anúncios que apresentam erros ou que estão demorando muito para carregar. |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | Classe. Os novos metadados do DRM estão associados ao item atual. |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | Classe. As informações de download estão disponíveis para o fluxo de mídia atual que está sendo reproduzido. |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | Classe. Um item de media player foi criado. |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | Classe. Uma operação de carregamento foi concluída. Despachado por `MediaPlayerItemLoader` para notificar seus clientes. |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | Classe. O status do player de mídia foi alterado. |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | Classe. O `MediaPlayerView` foi clicado. |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | Classe. A taxa de reprodução do player de mídia muda. |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | Classe. O algoritmo de switching de taxa de bits adaptável do player de mídia mudou para outro perfil devido às condições da rede ou da máquina. |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | Classe. O player iniciou a busca ou a operação de busca foi concluída. |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | Classe. O tamanho do vídeo está disponível. |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | Classe. O status do player de mídia foi alterado. |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | Classe. Os metadados cronometrados são processados pelo detector de oportunidades. |
| [TimelineEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | Classe. A linha do tempo do media player mudou. |