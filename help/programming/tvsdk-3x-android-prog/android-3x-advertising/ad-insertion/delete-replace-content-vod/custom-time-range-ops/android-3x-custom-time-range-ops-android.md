---
description: A classe CustomRangeMetadata identifica diferentes tipos de intervalos de tempo em uma marca de fluxo de VOD, exclusão e substituição. Para cada um desses tipos de intervalo de tempo personalizados, você pode executar as operações correspondentes, incluindo a exclusão e substituição de conteúdo de anúncio.
title: Operações de intervalo de tempo personalizado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Operações de intervalo de tempo personalizado {#custom-time-range-operations}

A classe CustomRangeMetadata identifica diferentes tipos de intervalos de tempo em um fluxo de VOD: marcar, excluir e substituir. Para cada um desses tipos de intervalo de tempo personalizados, você pode executar as operações correspondentes, incluindo a exclusão e substituição de conteúdo de anúncio.

<!--<a id="section_1323C0BAC259424C85A6ACFB48FE77EC"></a>-->

Para exclusão e substituição de anúncios, o TVSDK usa o seguinte *operação de intervalo de tempo personalizado* modos:

* **MARCAR** Esse modo era chamado de marcadores de anúncios personalizados em versões anteriores do TVSDK. O modo marca o início e o fim dos anúncios que já foram colocados no fluxo de VOD. Quando houver marcadores de intervalo de tempo do tipo `MARK` no fluxo, uma colocação inicial de `Mode.MARK` é gerado por `CustomMarkerOpportunityGenerator` e resolvido por `CustomRangeResolver`. Nenhum anúncio foi inserido.

* **DELETE** Para `DELETE` intervalos de tempo, uma variável `placementInformation` do tipo `Mode.DELETE` é criado e resolvido por `CustomRangeResolver`. `DeleteRangeTimelineOperation` define os intervalos a serem removidos da linha do tempo e o TVSDK usa `removeByLocalTime` da API do Mecanismo de vídeo de Adobe (AVE) para concluir esta operação. Se houver intervalos de DELETE e metadados de decisão de anúncios do Adobe Primetime, os intervalos serão excluídos primeiro, depois o `AuditudeResolver` O resolve anúncios usando o fluxo de trabalho típico do Adobe Primetime ad decisioning.

* **SUBSTITUIR** Para `REPLACE` intervalos de tempo, dois valores iniciais `placementInformations` são criados, um `Mode.DELETE` e um `Mode.REPLACE`. `CustomRangeResolver` exclui os intervalos de tempo primeiro e, em seguida, a variável `AuditudeResolver` insere anúncios do `replaceDuration` na linha do tempo. Se não `replaceDuration` for especificado, o servidor determinará o que inserir.

Para oferecer suporte a essas operações personalizadas de intervalo de tempo, o TVSDK fornece o seguinte:

* Vários resolvedores de conteúdo

  Um fluxo pode ter vários resolvedores de conteúdo com base no modo de sinalização de anúncios e nos metadados de anúncios. O comportamento muda com diferentes combinações de modos de sinalização de anúncios e metadados de anúncios.
* Várias oportunidades iniciais usando o `CustomMarkerOpportunityGenerator`.
* Um novo modo de sinalização de anúncio, `CUSTOM_RANGES`.

  Os anúncios são colocados com base nos dados de Intervalo de tempo de uma fonte externa, como um arquivo JSON.
