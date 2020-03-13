---
description: A classe CustomRangeMetadata identifica tipos diferentes de intervalos de tempo em uma marca de fluxo VOD, excluir e substituir. Para cada um desses tipos de intervalo de tempo personalizado, é possível executar operações correspondentes, incluindo a exclusão e substituição do conteúdo do anúncio.
seo-description: A classe CustomRangeMetadata identifica tipos diferentes de intervalos de tempo em uma marca de fluxo VOD, excluir e substituir. Para cada um desses tipos de intervalo de tempo personalizado, é possível executar operações correspondentes, incluindo a exclusão e substituição do conteúdo do anúncio.
seo-title: Operações de intervalo de tempo personalizado
title: Operações de intervalo de tempo personalizado
uuid: eadd4d8d-0e03-40ca-ae3b-eede82bf2df8
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Operações de intervalo de tempo personalizado {#custom-time-range-operations}

A classe CustomRangeMetadata identifica tipos diferentes de intervalos de tempo em um fluxo VOD: marcar, excluir e substituir. Para cada um desses tipos de intervalo de tempo personalizado, é possível executar operações correspondentes, incluindo a exclusão e substituição do conteúdo do anúncio.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Para exclusão e substituição de anúncios, o TVSDK usa os seguintes modos de operação *de intervalo de tempo* personalizado:

* **MARK** Esse modo era conhecido como marcadores de anúncio personalizados em versões anteriores do TVSDK. O modo marca as horas de início e término dos anúncios que já foram colocados no fluxo VOD. Quando há marcadores de intervalo de tempo do tipo `MARK` no fluxo, uma disposição inicial de `Mode.MARK` é gerada por `CustomMarkerOpportunityGenerator` e resolvida por `CustomRangeResolver`. Nenhuma publicidade é inserida.

* **EXCLUIR** Para intervalos de tempo, um `DELETE` tipo inicial `placementInformation` é criado e resolvido por `Mode.DELETE` `CustomRangeResolver`. `DeleteRangeTimelineOperation` define os intervalos a serem removidos da linha do tempo e o TVSDK usa `removeByLocalTime` a API do Adobe Video Engine (AVE) para concluir esta operação. Se houver intervalos DELETE e metadados de decisão de anúncio do Adobe Primetime, os intervalos serão excluídos primeiro e, em seguida, eles `AuditudeResolver` resolverão publicidades usando o fluxo de trabalho de decisão de anúncio típico do Adobe Primetime.

* **SUBSTITUIR** Para `REPLACE` intervalos de tempo, dois `placementInformations` são criados, um `Mode.DELETE` e um `Mode.REPLACE`. `CustomRangeResolver` exclui os intervalos de tempo primeiro e, em seguida, `AuditudeResolver` insere publicidades do especificado `replaceDuration` na linha do tempo. Se nenhum `replaceDuration` for especificado, o servidor determinará o que inserir.

Para suportar essas operações de intervalo de tempo personalizado, o TVSDK fornece o seguinte:

* Vários resolvedores de conteúdo

   Um fluxo pode ter vários resolvedores de conteúdo com base no modo de sinalização do anúncio e nos metadados do anúncio. O comportamento muda com diferentes combinações de modos de sinalização de anúncio e metadados de anúncio.
* Várias oportunidades iniciais usando `CustomMarkerOpportunityGenerator`.
* Um novo modo de sinalização de anúncios, `CUSTOM_RANGES`.

   Os anúncios são colocados com base nos dados de Intervalo de tempo de uma fonte externa, como um arquivo JSON.