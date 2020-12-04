---
description: O TVSDK despacha eventos de serviço de anúncios em resposta a operações de metadados programados.
seo-description: O TVSDK despacha eventos de serviço de anúncios em resposta a operações de metadados programados.
seo-title: Eventos de metadados de veiculação/agendamento de anúncio
title: Eventos de metadados de veiculação/agendamento de anúncio
uuid: fd50a937-0c9b-4c47-acb2-1ffc0592ad54
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Eventos de metadados de veiculação/agendamento de anúncio{#ad-serving-timed-metadata-events}

O TVSDK despacha eventos de serviço de anúncios em resposta a operações de metadados programados.

Para ser notificado sobre todos esses eventos relacionados, registre os ouvintes de eventos com o objeto `MediaPlayer` para os seguintes eventos.

| Evento | Significado |
|---|---|
| TimedMetadataEvent.[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | Metadados cronometrados ID3 foram processados. |
| TimedMetadataEvent.[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | Metadados cronometrados foram processados e nenhuma oportunidade foi detectada. |
| TimedMetadataEvent.[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | Metadados cronometrados estão disponíveis e nenhuma oportunidade foi detectada. |
| TimedMetadataEvent.[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | Metadados cronometrados foram processados e nenhuma oportunidade foi detectada no manifesto em segundo plano. |