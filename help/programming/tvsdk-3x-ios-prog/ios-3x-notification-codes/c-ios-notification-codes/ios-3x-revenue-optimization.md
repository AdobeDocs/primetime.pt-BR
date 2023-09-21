---
description: Esta tabela fornece informações detalhadas sobre as notificações de Otimização de Receita.
title: Código de otimização de RECEITA
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Código de otimização de RECEITA {#revenue-optimization-code}

Esta tabela fornece informações detalhadas sobre notificações de OTIMIZAÇÃO DE RECEITA.

## Habilitar Relatórios de Otimização de Receita {#enable-revenue-optimization-reporting}

Para ativar esse relatório, use a API PTMediaPlayer: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>A maioria das notificações informativas contém metadados relevantes, por exemplo, o URL do recurso que falhou no download. Algumas notificações contêm metadados para especificar se o problema ocorreu no conteúdo de vídeo principal, no conteúdo de áudio alternativo ou em um anúncio.

| Código | Nome | Notificação interna | Chaves de metadados | Comentários |
|---|---|---|---|---|
| 401001 | REVENUE_OTIMIZATION_REPORTING | Nenhum | Consulte a tabela abaixo para obter as chaves de metadados com base em eventos diferentes. | Nenhum |

| Detalhes do evento | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** Despachado no TVSDK quando MediaPlayer::replaceCurrentResource é chamado. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, evento, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackagingEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** Despachado no TVSDK quando o conteúdo entrou no estado preparado e está pronto para reprodução. Esse evento não será despachado em cada upload de manifesto - será despachado somente na carga inicial. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** Despachado no TVSDK quando uma oportunidade é gerada. | clientTimestamp, evento, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** Despachado no TVSDK quando uma oportunidade começa a ser resolvida. | clientTimestamp, evento, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** Despachado no TVSDK quando um resolvedor de anúncios chama MediaPlayerClient::notifyFailed(). Necessidade de preencher dados | opportunityId, notificationAD |
| **AD_RESOURCE_LOAD** Despachado quando qualquer recurso de anúncio é buscado pelo URL. responseStartTime: Carimbo de data e hora de Unix para quando a solicitação foi iniciada pela primeira vez. responseTotalTime: Tempo total (em segundos) necessário para uma resposta ser carregada. responseStatus: o código de status encontrado durante a busca do recurso. status: &quot;error&quot; ou &quot;success&quot; referrerAdId: a id do anúncio de referência que solicitou a busca deste recurso (se presente). referrerUrl: o url de referência que solicitou a busca deste recurso. errorMessage:Se o status for &quot;error&quot;, o motivo do erro estará localizado aqui. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** Despachado no TVSDK quando um CRS é aplicado a um ativo, bem como a resposta para o m3u8. resourceType:sempre &quot;crs&quot;. responseStartTime: Carimbo de data e hora de Unix para quando a solicitação foi iniciada pela primeira vez. responseTotalTime: Tempo total (em segundos) necessário para uma resposta ser carregada. responseStatus: o código de status encontrado durante a busca do recurso. status:&quot;erro&quot; ou &quot;sucesso&quot;. errorMessage:Se o status for &quot;error&quot;, o motivo do erro estará localizado aqui. mediaFileUrl: o url do arquivo de mídia original que foi selecionado. mediaFileBitrate:a taxa de bits do arquivo de mídia que foi selecionado. mediaFileMimeType: o tipo mime do arquivo de mídia selecionado. url:o url final do ativo. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** Despachado no TVSDK depois que um adBreak foi colocado na linha do tempo. Esse evento ocorrerá uma vez para cada ad break. tempoProposta: a hora em que o intervalo comercial foi solicitado para ser colocado. atualTime: a hora em que o ad break foi realmente colocado. posedDuration: a duração do ad break solicitado para inserção. Para o conteúdo em tempo real, essa seria a duração da sinalização. Para conteúdo de VOD, normalmente seria -1. atualDuration: a duração real do ad break inserido. Calculada como a duração da soma de todos os anúncios, definida pelas respectivas durações de segmento, adicionados ou substituídos na linha do tempo do fluxo original. proposedAds:O número de anúncios no ad break proposto. totalAds: o número de anúncios colocados com êxito. ads...n:Os anúncios inseridos com êxito serão inseridos aqui. Informações completas do manifesto de anúncio podem ser recuperadas de AD_OPPORTUNITY_RESOLVE_PROCESS | opportunityId, status, errorMessage, posedTime, proposedDuration, atualTime, atualDuration, proposedAds, totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_START** Despachado no TVSDK após o início da reprodução de um anúncio. | clientTimestamp, evento, id, url, duração, tipo, opportunityId, clientId |
| **AD_PLAYBACK_COMPLETE** Despachado no TVSDK depois que um anúncio conclui a reprodução. | clientTimestamp, evento, id, url, duração, tipo, opportunityId, clientId |
| **ADBREAK_PLAYBACK_START** Despachado no TVSDK quando um adbreak inicia a reprodução. | clientTimestamp, evento, opportunityId, duração, tempo, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** Despachado no TVSDK quando um adbreak conclui a reprodução. | clientTimestamp, evento, opportunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** Despachado no TVSDK quando qualquer conteúdo é concluído.Isso pode ocorrer se o fluxo for substituído, o reprodutor entrar em um estado de erro, o reprodutor for redefinido ou o conteúdo for realmente concluído. Esse evento será necessário para rastrear uma sessionId. | clientTimestamp, evento, clientId, url, status, errorMessage |
| **AD_REPRODUZIR_ERRO** Despachado no TVSDK quando um anúncio tem um erro ao ser reproduzido (erros de fluxo de variante). | event, error, Timestamp, manifestUrl, time, opportunityId, url |
