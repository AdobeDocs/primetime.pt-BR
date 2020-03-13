---
description: O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.
seo-description: O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.
seo-title: Operações de intervalo de tempo personalizado
title: Operações de intervalo de tempo personalizado
uuid: e04af786-8dac-41a6-8406-f2ca04f612a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Operações de intervalo de tempo personalizado {#custom-time-range-operations}

O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.

O recurso excluir e substituir estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionados a anúncios. Além de marcar esses intervalos de tempo, também é possível excluir e substituir intervalos de tempo.

A exclusão e substituição de anúncios é implementada com `TimeRange` elementos que identificam diferentes tipos de intervalos de tempo em um fluxo VOD: marcar, excluir e substituir. Para cada um desses tipos de intervalo de tempo personalizado, é possível executar operações correspondentes, incluindo a exclusão e substituição do conteúdo do anúncio.

Para exclusão e substituição de anúncios, o TVSDK usa os seguintes modos de operação *de intervalo de tempo* personalizado:

* **MARK**(esses foram chamados de marcadores de anúncio personalizados em versões anteriores do TVSDK). Eles marcam os tempos de início e término para anúncios que já foram colocados no fluxo VOD. Quando há marcadores de intervalo de tempo do tipo MARK no fluxo, uma disposição inicial de `Mode.MARK` é gerada e resolvida pelo `CustomAdMarkersContentResolver`. Nenhuma publicidade é inserida.

* **DELETE** Para EXCLUIR intervalos de tempo, um tipo inicial `placementInformation` do tipo `Mode.DELETE` é criado e resolvido pelo correspondente `DeleteContentResolver`. `ContentRemoval` é um novo `timelineOperation` que define os intervalos a serem removidos da linha do tempo. O TVSDK usa `removeByLocalTime` a API do Adobe Video Engine (AVE) para facilitar essa operação. Se houver intervalos DELETE e metadados de decisão de anúncio do Adobe Primetime (anteriormente conhecidos como Auditude), os intervalos serão excluídos primeiro e, em seguida, os anúncios `AuditudeResolver` serão resolvidos usando o fluxo de trabalho normal de decisão de anúncio do Adobe Primetime.

* **SUBSTITUIR** por intervalos de tempo SUBSTITUIR, dois `placementInformations` são criados, um `Mode.DELETE` e um `Mode.REPLACE`. O `DeleteContentResolver` exclui os intervalos de tempo primeiro e, em seguida, `AuditudeResolver` insere publicidades do especificado `replaceDuration` na linha do tempo. Se nenhum `replaceDuration` for especificado, o servidor determinará o que inserir.

Para suportar essas operações de intervalo de tempo personalizado, o TVSDK fornece o seguinte:

* Vários resolvedores de conteúdo

   Um fluxo pode ter vários resolvedores de conteúdo com base no modo de sinalização do anúncio e nos metadados do anúncio. O comportamento muda com diferentes combinações de modos de sinalização de anúncio e metadados de anúncio.
* Vários iniciais `PlacementInformations` A `DefaultMediaPlayer` cria uma lista inicial `PlacementInformations` com base no modo de sinalização do anúncio e nos metadados do anúncio a serem resolvidos pela `MediaPlayerClient`.

* Novo modo de sinalização de anúncio: Intervalos de tempo personalizados

   Os anúncios são colocados com base nos dados de Intervalo de tempo de uma fonte externa (como um arquivo JSON).