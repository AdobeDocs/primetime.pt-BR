---
description: 'Esta tabela fornece informações detalhadas sobre notificações de Otimização de Receita. '
seo-description: 'Esta tabela fornece informações detalhadas sobre notificações de Otimização de Receita. '
seo-title: Código de Otimização de RECEITA
title: Código de Otimização de RECEITA
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Código de Otimização de RECEITA {#revenue-optimization-code}

Esta tabela fornece informações detalhadas sobre notificações de OTIMIZAÇÃO DE RECEITA.

## Ativar relatório de otimização de receita {#enable-revenue-optimization-reporting}

Para ativar esse relatório, use a api PTMediaPlayer: `[mediaPlayer
setRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

[!NObservação]: A maioria das notificações informativas contém metadados relevantes, por exemplo, o URL do recurso que falhou ao baixar. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

|Código|Nome|Notificação interna|Teclas de metadados|Observações||—|—|—|—|401001| RECEITA_OTIMIZAÇÃO_RELATÓRIO| Nenhum| Consulte a tabela abaixo para obter as chaves de metadados com base em eventos diferentes. | Nenhum|

| Detalhes do evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** Despachado no TVSDK quando MediaPlayer::replaceCurrentResource é chamado. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, RepackEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** despachado no TVSDK quando o conteúdo entrou no estado preparado e está pronto para a reprodução. Esse evento não será despachado em todos os carregamentos do manifesto - só será despachado na carga inicial. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** Despachado no TVSDK quando uma oportunidade é gerada. | clientTimestamp, event, portunityId, placementDuration, clientId |
| **AD_OPORTUNITY_RESOLVE_START** Despachado no TVSDK quando uma oportunidade começa a ser resolvida. | clientTimestamp, event, portunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** despachado no TVSDK quando um resolvedor de publicidade chama MediaPlayerClient::notificationFailed(). Necessidade de preencher os dados | offerId, notificationAD |
| **AD_RESOURCE_LOAD** Despachado quando qualquer recurso de anúncio é obtido pelo URL. responseStartTime:Carimbo de data e hora Unix para quando a solicitação foi iniciada pela primeira vez. responseTotalTime:Quantidade total de tempo (em segundos) que uma resposta levou para carregar. responseStatus:O código de status encontrado ao buscar o recurso. status: &quot;error&quot; ou &quot;success&quot; referrerAdId:A ID do anúncio de referência que solicitou a busca deste recurso (se presente). referrerUrl:O url de referência que solicitou a busca deste recurso. errorMessage:Se o status for &quot;error&quot;, o motivo do erro será localizado aqui. | offerId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** Despachado no TVSDK quando um CRS é aplicado a um ativo, bem como a resposta para m3u8. resourceType:always &quot;crs&quot;. responseStartTime:Carimbo de data e hora Unix para quando a solicitação foi iniciada pela primeira vez. responseTotalTime:Quantidade total de tempo (em segundos) que uma resposta levou para carregar. responseStatus:O código de status encontrado ao buscar o recurso. status: &quot;error&quot; ou &quot;success&quot;. errorMessage:Se o status for &quot;error&quot;, o motivo do erro será localizado aqui. mediaFileUrl:O url do arquivo de mídia original selecionado. mediaFileBitrate:A taxa de bits do arquivo de mídia selecionado. mediaFileMimeType: O tipo mime do arquivo de mídia selecionado. url:O url do ativo final. | offerId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** Despachado no TVSDK após um adBreak ser colocado na linha do tempo. Esse evento ocorrerá uma vez para cada pausa de anúncio. offerTime:A hora em que a pausa do anúncio foi solicitada para ser colocada. actualTime:A hora em que o intervalo comercial foi realmente colocado. offerDuration:A duração do intervalo de anúncios que foi solicitado para inserção. Para conteúdo ao vivo, essa seria a duração da dica. Para o conteúdo VOD, normalmente seria -1. actualDuration:A duração real do intervalo do anúncio inserido. Calculada como a duração da soma de todos os anúncios, definida pelas respectivas durações de segmento, adicionada ou substituída na linha do tempo do fluxo original. propostas:O número de anúncios no intervalo de anúncios proposto. totalAds:O número de anúncios que foram colocados com êxito. publicidades...n:As publicidades inseridas com êxito serão inseridas aqui. Informações completas do manifesto de anúncio podem ser recuperadas de AD_OPPORTUNITY_RESOLVE_PROCESS | possibleId, status, errorMessage, offerTime, offerDuration, actualTime, actualDuration, tentAds, totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_START** despachado no TVSDK após o início da reprodução de um anúncio. | clientTimestamp, event, id, url, duration, type, portunityId, clientId |
| **AD_PLAYBACK_COMPLETE** despachado no TVSDK após a conclusão da reprodução de um anúncio. | clientTimestamp, event, id, url, duration, type, portunityId, clientId |
| **ADBREAK_PLAYBACK_START** despachado no TVSDK quando um adbreak inicia a reprodução. | clientTimestamp, event, portunityId, duration, time, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** despachado no TVSDK quando um adbreak conclui a reprodução. | clientTimestamp, event, portunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** Despachado no TVSDK quando qualquer conteúdo é concluído. Isso pode ocorrer se o fluxo for substituído, o player inserir um estado de erro, o player for redefinido ou o conteúdo for realmente concluído. Esse evento será necessário para rastrear uma sessionId. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** Despachado no TVSDK quando um anúncio apresenta um erro de reprodução (erros de fluxo de variação). | event, error, Timestamp, manifestUrl, time, portunityId, url |