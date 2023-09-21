---
description: O TVSDK despacha eventos de veiculação de anúncios em resposta a operações de metadados cronometradas.
title: Eventos de metadados de veiculação/temporizados de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Eventos de metadados de veiculação/temporizados de anúncios{#ad-serving-timed-metadata-events}

O TVSDK despacha eventos de veiculação de anúncios em resposta a operações de metadados cronometradas.

Para ser notificado sobre todos esses eventos relacionados, registre os ouvintes de eventos na `MediaPlayer` para os eventos a seguir.

| Evento | Significado |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Um metadado de tempo ID3 foi processado. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | Metadados cronometrados foram processados e nenhuma oportunidade foi detectada. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | Os metadados cronometrados estão disponíveis e nenhuma oportunidade foi detectada. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Os metadados cronometrados foram processados e nenhuma oportunidade foi detectada no manifesto em segundo plano. |
