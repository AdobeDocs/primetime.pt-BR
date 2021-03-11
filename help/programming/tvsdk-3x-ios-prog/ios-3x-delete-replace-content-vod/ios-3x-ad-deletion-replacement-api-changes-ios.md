---
description: O TVSDK oferece suporte à exclusão programática e substituição de conteúdo de anúncio em fluxos VOD.
title: Exclusão de anúncios e alterações da API de substituição
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Exclusão de anúncio e alterações de substituição da API {#ad-deletion-and-replacement-api-changes}

O TVSDK oferece suporte à exclusão programática e substituição de conteúdo de anúncio em fluxos VOD.

O recurso excluir e substituir estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionado a anúncios. Além de marcar esses intervalos de tempo, também é possível excluir e substituir intervalos de tempo.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

As alterações a seguir no TVSDK são compatíveis com exclusão e substituição de anúncios.

**Novas APIs**

* `PTTimeRangeCollection` é uma classe pública que define um conjunto predefinido de intervalos e um tipo:

   * `property PTTimeRangeCollectionType type` indica o tipo de intervalo de tempo.
   * `property NSArray* ranges` é usada para definir os intervalos de tempo.

      O tipo esperado de objetos na matriz é `PTReplacementTimeRange` ou `CMTimeRange`.

      >[!TIP]
      >
      >Todos os objetos da matriz devem ser do mesmo tipo.

   * `PTTimeRangeCollectionType` é um enum que define o comportamento dos intervalos definidos no  `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: O tipo dos intervalos é  *Mark*. Os intervalos são usados para marcar os intervalos no conteúdo como Anúncios.

      * `PTTimeRangeCollectionTypeDeleteRanges`: O tipo dos intervalos é Delete. Os intervalos definidos são removidos do conteúdo principal antes da inserção do anúncio.
      * `PTTimeRangeCollectionTypeReplaceRanges`: O tipo dos intervalos é Replace. Os intervalos definidos são substituídos do principal por Anúncios (o modo de sinalização do anúncio é definido como `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nova classe pública que define um único intervalo de  `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Define o início e a duração do intervalo.
   * `property long replacementDuration` - Se o tipo de  `TimeRangeCollection` for  `PTTimeRangeCollectionTypeReplaceRanges`,  `replacementDuration` será usado para criar uma oportunidade de disposição (inserção de anúncio) com uma duração de  `replacementDuration`. Se `replacementDuration` não estiver definido, o servidor de publicidade determinará a duração e o número de anúncios para essa oportunidade de posicionamento.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - Adição de um novo tipo de  `PTAdSignalingMode`. Esse modo é usado em conjunto com o `PTTimeRangeCollection` com o tipo `PTTimeRangeCollectionReplace` para inserção de anúncio com base nos intervalos de substituição.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - Para definir os intervalos de tempo usados nos intervalos marcar/excluir/substituir no conteúdo da reprodução.

* Logs de aviso:

   * `UNDEFINED_TIME_RANGES`

      * Tipo - Aviso
      * Descrição - O modo de sinalização de anúncio é definido como intervalos personalizados, mas os intervalos personalizados não são definidos.
   * `INVALID_TIME_RANGES`

      * Tipo - Aviso
      * Descrição - Um ou mais intervalos de tempo são inválidos e serão ignorados ou modificados.


**APIs obsoletas**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Essa propriedade era usada anteriormente para definir intervalos C3 para marcação. Agora está obsoleto, pois esses intervalos são definidos por `PTTimeRangeCollection`.