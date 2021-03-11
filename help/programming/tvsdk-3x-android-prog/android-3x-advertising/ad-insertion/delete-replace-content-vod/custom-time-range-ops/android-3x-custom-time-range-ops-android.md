---
description: A classe CustomRangeMetadata identifica diferentes tipos de intervalos de tempo em uma marca de fluxo de VOD, excluir e substituir. Para cada um desses tipos de intervalo de tempo personalizado, é possível executar operações correspondentes, incluindo a exclusão e substituição do conteúdo do anúncio.
title: Operações de intervalo de tempo personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Operações personalizadas de intervalo de tempo {#custom-time-range-operations}

A classe CustomRangeMetadata identifica diferentes tipos de intervalos de tempo em um fluxo de VOD: marcar, excluir e substituir. Para cada um desses tipos de intervalo de tempo personalizado, é possível executar operações correspondentes, incluindo a exclusão e substituição do conteúdo do anúncio.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Para exclusão e substituição de anúncios, o TVSDK usa os seguintes modos *operação de intervalo de tempo personalizado*:

* **** MARKT: esse modo era conhecido como marcadores de anúncio personalizados em versões anteriores do TVSDK. O modo marca os horários de início e término dos anúncios que já foram colocados no fluxo de VOD. Quando há marcadores de intervalo de tempo do tipo `MARK` no fluxo, uma disposição inicial de `Mode.MARK` é gerada por `CustomMarkerOpportunityGenerator` e resolvida por `CustomRangeResolver`. Nenhuma publicidade é inserida.

* **** DELETEFou intervalos de  `DELETE` tempo, um tipo inicial  `placementInformation` de  `Mode.DELETE` é criado e resolvido por  `CustomRangeResolver`. `DeleteRangeTimelineOperation` define os intervalos a serem removidos da linha do tempo e o TVSDK usa a  `removeByLocalTime` partir da API do mecanismo de vídeo do Adobe (AVE) para concluir essa operação. Se houver intervalos de DELETE e metadados de decisão de anúncio do Adobe Primetime, os intervalos serão excluídos primeiro e `AuditudeResolver` resolverá anúncios usando o fluxo de trabalho típico de decisão de anúncio do Adobe Primetime.

* **** REPLACEFou intervalos de  `REPLACE` tempo, duas  `placementInformations` são criadas, uma  `Mode.DELETE` e uma  `Mode.REPLACE`. `CustomRangeResolver` exclui os intervalos de tempo primeiro e, em seguida,  `AuditudeResolver` insere anúncios do especificado  `replaceDuration` na linha do tempo. Se nenhum `replaceDuration` for especificado, o servidor determinará o que inserir.

Para suportar essas operações de intervalo de tempo personalizado, o TVSDK fornece o seguinte:

* Vários resolvedores de conteúdo

   Um fluxo pode ter vários resolvedores de conteúdo com base no modo de sinalização de anúncio e nos metadados do anúncio. O comportamento muda com diferentes combinações de modos de sinalização de anúncio e metadados de anúncio.
* Várias oportunidades iniciais usando `CustomMarkerOpportunityGenerator`.
* Um novo modo de sinalização de anúncio, `CUSTOM_RANGES`.

   Os anúncios são colocados com base nos dados de Intervalo de tempo de uma fonte externa, como um arquivo JSON.