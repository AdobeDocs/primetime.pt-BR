---
description: O TVSDK despacha eventos de veiculação de anúncios em resposta a operações de metadados cronometrados.
title: Eventos de metadados de veiculação de anúncios/cronometragem
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Eventos de metadados de veiculação/hora de anúncio{#ad-serving-timed-metadata-events}

O TVSDK despacha eventos de veiculação de anúncios em resposta a operações de metadados cronometrados.

Para ser notificado sobre todos esses eventos relacionados, registre ouvintes de eventos com o objeto `MediaPlayer` para os seguintes eventos.

| Evento | Significado |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Metadados cronometrados ID3 foram processados. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | Metadados cronometrados foram processados e nenhuma oportunidade foi detectada. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | Metadados cronometrados estão disponíveis e nenhuma oportunidade foi detectada. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Metadados cronometrados foram processados e nenhuma oportunidade foi detectada no manifesto em segundo plano. |