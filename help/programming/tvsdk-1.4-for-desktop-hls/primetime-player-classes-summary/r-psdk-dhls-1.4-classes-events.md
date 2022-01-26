---
description: Essas classes descrevem eventos que o TVSDK envia para o seu reprodutor de mídia em resposta a várias atividades.
title: Classes de eventos
exl-id: a349984a-5e47-4895-a56f-ef25eb372c79
source-git-commit: 776d3d1668f063f1595bd3ecb53603171905014a
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Classes de eventos {#events-classes}

Essas classes descrevem eventos que o TVSDK envia para o seu reprodutor de mídia em resposta a várias atividades.

Pacote: [com.adobe.mediacore.events](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/package-detail.html)

| Nome | Significado |
|---|---|
| [AdBreakPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html) | Classe. Um ad break foi iniciado ou concluído. |
| [AdClickEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html) | Classe. O usuário clicou em um anúncio. |
| [AdPlaybackEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html) | Classe. O reprodutor reproduziu um anúncio. |
| [BufferEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html) | Classe. O reprodutor iniciou ou parou o buffering. |
| [CustomAdEvent](https://experienceleague.adobe.com/docs/primetime/programming/tvsdk-1-4-for-desktop-hls/advertising/custom-ads/r-psdk-dhls-1.4-custom-ad-events.html?lang=en) | Classe. O reprodutor exibe o status de carregamento do anúncio personalizado e pode ignorar anúncios que tenham erros ou que estejam demorando muito para serem carregados. |
| [DRMMetadataInfoEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html) | Classe. Os novos metadados de DRM estão associados ao item atual. |
| [LoadInformationEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/LoadInformationEvent.html) | Classe. As informações de download estão disponíveis para o fluxo de mídia atual que está sendo reproduzido. |
| [MediaPlayerItemEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html) | Classe. Um item do reprodutor de mídia foi criado. |
| [MediaPlayerItemLoaderEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemLoaderEvent.html) | Classe. Uma operação de carregamento foi concluída. Despachado por `MediaPlayerItemLoader` para notificar seus clientes. |
| [MediaPlayerStatusChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html) | Classe. O status do reprodutor de mídia foi alterado. |
| [MediaPlayerViewEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerViewEvent.html) | Classe. O `MediaPlayerView` foi clicado. |
| [PlaybackRateEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html) | Classe. A taxa de reprodução do reprodutor de mídia é alterada. |
| [ProfileEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html) | Classe. O algoritmo de switching de taxa de bits adaptável do reprodutor de mídia mudou para outro perfil devido às condições da rede ou da máquina. |
| [SeekEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html) | Classe. O reprodutor iniciou a busca ou a operação de busca foi concluída. |
| [SizeAvailableEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SizeAvailableEvent.html) | Classe. O tamanho do vídeo está disponível. |
| [TimeChangeEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html) | Classe. O status do reprodutor de mídia foi alterado. |
| [TimedMetadataEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html) | Classe. Os metadados cronometrados são processados pelo detector de oportunidade. |
| [TimelineEvent](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html) | Classe. A linha do tempo do reprodutor de mídia foi alterada. |
