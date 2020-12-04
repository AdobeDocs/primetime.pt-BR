---
description: O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.
seo-description: O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.
seo-title: Excluir e substituir publicidades em fluxos VOD
title: Excluir e substituir publicidades em fluxos VOD
uuid: 8f51c413-a8c9-46c1-aec6-0d536feaaeb7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# A exclusão de anúncios e as alterações de API de substituição {#ad-deletion-and-replacement-api-changes}

O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.

O recurso excluir e substituir estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionados a anúncios. Além de marcar esses intervalos de tempo, também é possível excluir e substituir intervalos de tempo.

As seguintes alterações no TVSDK oferecem suporte à exclusão e substituição.

**Novas APIs**

* `PTTimeRangeCollection` é uma classe pública que define um conjunto predefinido de intervalos e um tipo:

   * `property PTTimeRangeCollectionType type` indica o tipo de intervalo de tempo.
   * `property NSArray* ranges` é usada para definir os intervalos de tempo.

      O tipo esperado de objetos na matriz é `PTReplacementTimeRange` ou `CMTimeRange`.

      >[!TIP]
      >
      >Todos os objetos da matriz devem ser do mesmo tipo.

   * `PTTimeRangeCollectionType` é uma enumeração que define o comportamento para os intervalos definidos na variável  `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: O tipo dos intervalos é  *Mark*. Os intervalos são usados para marcar os intervalos no conteúdo como Anúncios.

      * `PTTimeRangeCollectionTypeDeleteRanges`: O tipo dos intervalos é Excluir. Os intervalos definidos são removidos do conteúdo principal antes da inserção do anúncio.
      * `PTTimeRangeCollectionTypeReplaceRanges`: O tipo dos intervalos é Substituir. Os intervalos definidos são substituídos do principal por Anúncios (o modo de sinalização de anúncios está definido para `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nova classe pública que define uma única faixa de  `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Define o start e a duração do intervalo.
   * `property long replacementDuration` - Se o tipo de evento  `TimeRangeCollection` for  `PTTimeRangeCollectionTypeReplaceRanges`, o  `replacementDuration` será usado para criar uma oportunidade de colocação (inserção de anúncio) com uma duração de  `replacementDuration`. Se `replacementDuration` não estiver definido, o servidor de publicidade determinará a duração e o número de anúncios para essa oportunidade de posicionamento.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - Adicionado um novo tipo de  `PTAdSignalingMode`. Esse modo é usado em conjunto com `PTTimeRangeCollection` com o tipo `PTTimeRangeCollectionReplace` para inserção de anúncio com base nos intervalos de substituição.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - Para definir os intervalos de tempo usados nos intervalos de marcação/exclusão/substituição no conteúdo da reprodução.

* Registros de aviso:

   * `UNDEFINED_TIME_RANGES`

      * Tipo - Aviso
      * Descrição - O modo de sinalização de anúncio é definido como intervalos personalizados, mas os intervalos personalizados não são definidos.
   * `INVALID_TIME_RANGES`

      * Tipo - Aviso
      * Descrição - Um ou mais intervalos de tempo são inválidos e serão ignorados ou modificados.


**APIs obsoletas**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Essa propriedade era usada anteriormente para definir intervalos C3 para marcação. Agora está obsoleto, pois esses intervalos são definidos via `PTTimeRangeCollection`.