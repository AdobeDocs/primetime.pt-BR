---
description: O TVSDK é compatível com a exclusão e substituição programática de conteúdo de anúncios em fluxos VOD.
title: Operações de intervalo de tempo personalizado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Operações de intervalo de tempo personalizado {#custom-time-range-operations}

O TVSDK é compatível com a exclusão e substituição programática de conteúdo de anúncios em fluxos VOD.

O recurso de exclusão e substituição estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionados a anúncios. Além de marcar esses intervalos de tempo, você também pode excluir e substituir intervalos de tempo.

A exclusão e substituição de anúncios são implementadas com `TimeRange` elementos que identificam diferentes tipos de intervalos de tempo em um fluxo de VOD: marcar, excluir e substituir. Para cada um desses tipos de intervalo de tempo personalizados, você pode executar as operações correspondentes, incluindo a exclusão e substituição de conteúdo de anúncio.

Para exclusão e substituição de anúncios, o TVSDK usa o seguinte *operação de intervalo de tempo personalizado* modos:

* **MARCAR**
(Eles eram chamados de marcadores de anúncios personalizados em versões anteriores do TVSDK). Eles marcam o início e o fim dos anúncios que já foram colocados no fluxo de VOD. Quando houver marcadores de intervalo de tempo do tipo MARK no fluxo, uma posição inicial de `Mode.MARK` é gerado e resolvido pelo `CustomAdMarkersContentResolver`. Nenhum anúncio foi inserido.

* **DELETE**
Para intervalos de tempo de DELETE, uma variável `placementInformation` do tipo `Mode.DELETE` é criada e resolvida pela variável correspondente `DeleteContentResolver`. `ContentRemoval` é um novo `timelineOperation` que define os intervalos a serem removidos da linha do tempo. TVSDK usa `removeByLocalTime` da API do Mecanismo de vídeo de Adobe (AVE) para facilitar essa operação. Se houver metadados de intervalos de DELETE e Adobe Primetime ad decisioning (anteriormente conhecidos como Auditude), os intervalos serão excluídos primeiro e, em seguida, a variável `AuditudeResolver` resolve anúncios usando o fluxo de trabalho normal do Adobe Primetime ad decisioning.

* **SUBSTITUIR**
Para intervalos de tempo REPLACE, dois valores iniciais `placementInformations` são criados, um `Mode.DELETE` e um `Mode.REPLACE`. A variável `DeleteContentResolver` exclui os intervalos de tempo primeiro e, em seguida, a variável `AuditudeResolver` insere anúncios do `replaceDuration` na linha do tempo. Se não `replaceDuration` for especificado, o servidor determinará o que inserir.

Para oferecer suporte a essas operações personalizadas de intervalo de tempo, o TVSDK fornece o seguinte:

* Vários resolvedores de conteúdo

  Um fluxo pode ter vários resolvedores de conteúdo com base no modo de sinalização de anúncios e nos metadados de anúncios. O comportamento muda com diferentes combinações de modos de sinalização de anúncios e metadados de anúncios.
* Inicial múltipla `PlacementInformations` A variável `DefaultMediaPlayer` cria uma lista de valores iniciais `PlacementInformations` com base no modo de sinalização de anúncios e nos metadados de anúncios a serem `MediaPlayerClient`.

* Novo modo de sinalização de anúncio: intervalos de tempo personalizados

  Os anúncios são colocados com base nos dados de Intervalo de tempo de uma fonte externa (como um arquivo JSON).
