---
description: 'Esta tabela fornece informações detalhadas sobre notificações de Otimização de Receita. '
title: Código de otimização de receita
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# Código de otimização de receita {#revenue-optimization-code}

Esta tabela fornece informações detalhadas sobre notificações de OTIMIZAÇÃO DE RECEITA.

## Ativar Relatórios de Otimização de Receita {#enable-revenue-optimization-reporting}

Para ativar esse relatório, use a api PTMediaPlayer: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>A maioria das notificações informativas contém metadados relevantes, por exemplo, o URL do recurso que falhou no download. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

| Código | Nome | Notificação interna | Chaves de metadados | Comentários |
|---|---|---|---|---|
| 401001 | REVENUE_OTIMIZATION_REPORTING | Nenhum | Consulte a tabela abaixo para obter as chaves de metadados com base em eventos diferentes. | Nenhum |

| Detalhes do evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_** STARTDispatched no TVSDK quando MediaPlayer::replaceCurrentResource é chamado. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, RepackagingEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_** STARTDispatched no TVSDK quando o conteúdo entrou no estado preparado e está pronto para reprodução. Esse evento não será despachado em cada upload de manifesto - só será despachado na carga inicial. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_** GENERATEDDispatched em TVSDK quando uma oportunidade é gerada. | clientTimestamp, event, portunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_** STARTDispatched no TVSDK quando uma oportunidade começa a ser resolvida. | clientTimestamp, event, portunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_** FAILEDDispatched em TVSDK quando um resolvedor de anúncios chama MediaPlayerClient::notifyFailed(). Necessidade de preencher os dados | possibleId, notificationAD |
| **AD_RESOURCE_** LOADDispatched quando qualquer recurso de anúncio é buscado por URL. responseStartTime:Carimbo de data e hora Unix para quando a solicitação foi iniciada pela primeira vez. responseTotalTime:Quantidade total de tempo (em segundos) necessário para uma resposta ser carregada. responseStatus:O código de status encontrado ao buscar o recurso. status: &quot;error&quot; ou &quot;success&quot; referrerAdId:A id de anúncio de referência que solicitou a busca deste recurso (se presente). referrerUrl: o url de referência que solicitou a busca deste recurso. errorMessage:Se o status for &quot;error&quot;, o motivo do erro estará localizado aqui. | possibleId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_** CRSDispatched em TVSDK quando um CRS é aplicado a um ativo, bem como a resposta para m3u8. resourceType:always &quot;crs&quot;. responseStartTime:Carimbo de data e hora Unix para quando a solicitação foi iniciada pela primeira vez. responseTotalTime:Quantidade total de tempo (em segundos) necessário para uma resposta ser carregada. responseStatus:O código de status encontrado ao buscar o recurso. status: &quot;error&quot; ou &quot;success&quot;. errorMessage:Se o status for &quot;error&quot;, o motivo do erro estará localizado aqui. mediaFileUrl:o url do arquivo de mídia original selecionado. mediaFileBitrate:A taxa de bits do arquivo de mídia selecionado. mediaFileMimeType: O tipo MIME do arquivo de mídia selecionado. url: o url do ativo final. | possibleId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_** PLACEDispatched em TVSDK depois que um adBreak era colocado na linha do tempo. Esse evento ocorrerá uma vez para cada ad break. currentTime:A hora em que o ad break foi solicitado a ser colocado. atualTime:a hora em que o ad break foi realmente colocado. propostaDuração:A duração do ad break que foi solicitado para inserção. Para conteúdo ao vivo, essa seria a duração da sinalização. Para conteúdo VOD, normalmente seria -1. realDuration:A duração real do ad break inserido. Calculada como a duração da soma de todos os anúncios, definida por suas durações de segmento respectivas, adicionada ou substituída na linha do tempo do fluxo original. propostas de anúncios: o número de anúncios no ad break proposto. totalAds: o número de anúncios que foram colocados com êxito. anúncios..n:As publicidades inseridas com êxito serão inseridas aqui. Todas as informações de manifesto de anúncio podem ser recuperadas de AD_OPPORTUNITY_RESOLVE_PROCESS | possibleId, status, errorMessage, bidTime, Nomes, realTime, realDuration, propostasAds, totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_** STARTDispatched no TVSDK depois que um anúncio começa a reprodução. | clientTimestamp, event, id, url, duração, tipo, optionId, clientId |
| **AD_PLAYBACK_** COMPLETEDdespachado no TVSDK após a conclusão da reprodução de um anúncio. | clientTimestamp, event, id, url, duração, tipo, optionId, clientId |
| **ADBREAK_PLAYBACK_** STARTDispatched no TVSDK quando um adbreak inicia a reprodução. | clientTimestamp, event, portunityId, duração, tempo, clientId |
| **ADBREAK_PLAYBACK_** COMPLETEDdespachado em TVSDK quando um adbreak conclui a reprodução. | clientTimestamp, event, portunityId, clientId |
| **CONTENT_PLAYBACK_** COMPLETEDé despachado no TVSDK quando qualquer conteúdo é concluído. Isso pode ocorrer se o fluxo for substituído, o reprodutor entra em um estado de erro, o reprodutor é redefinido ou o conteúdo é realmente concluído. Esse evento será necessário para rastrear uma sessionId. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_** ERRORDé despachado no TVSDK quando um anúncio tem um erro de reprodução (erros de fluxo de variante). | evento, erro, Carimbo de data e hora, manifestUrl, tempo, ID da oportunidade, url |
