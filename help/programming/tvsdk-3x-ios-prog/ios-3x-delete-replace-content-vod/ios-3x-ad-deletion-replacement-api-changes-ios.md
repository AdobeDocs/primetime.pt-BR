---
description: O TVSDK é compatível com a exclusão e substituição programática de conteúdo de anúncios em fluxos VOD.
title: Alterações na exclusão de anúncios e na API de substituição
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Alterações na exclusão de anúncios e na API de substituição {#ad-deletion-and-replacement-api-changes}

O TVSDK é compatível com a exclusão e substituição programática de conteúdo de anúncios em fluxos VOD.

O recurso de exclusão e substituição estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionados a anúncios. Além de marcar esses intervalos de tempo, você também pode excluir e substituir intervalos de tempo.

<!--<a id="section_7A90BFE99F1A4D908D6DDB0B49FA1199"></a>-->

As seguintes alterações no TVSDK oferecem suporte à exclusão e substituição de anúncios.

**Novas APIs**

* `PTTimeRangeCollection` é uma classe pública que define um conjunto predefinido de intervalos e um tipo:

   * `property PTTimeRangeCollectionType type` indica o tipo de intervalo de tempo.
   * `property NSArray* ranges` é usado para definir os intervalos de tempo.

     Os tipos esperados de objetos na matriz são `PTReplacementTimeRange` ou `CMTimeRange`.

     >[!TIP]
     >
     >Todos os objetos da matriz devem ser do mesmo tipo.

   * `PTTimeRangeCollectionType` é um enum que define o comportamento dos intervalos definidos na variável `PTTimeRangeCollection`:

      * `PTTimeRangeCollectionTypeMarkRanges`: o tipo dos intervalos é *Marcar*. Os intervalos são usados para marcar os intervalos no conteúdo como Anúncios.

      * `PTTimeRangeCollectionTypeDeleteRanges`: o tipo dos intervalos é Excluir. Os intervalos definidos são removidos do conteúdo principal antes da inserção do anúncio.
      * `PTTimeRangeCollectionTypeReplaceRanges`: o tipo dos intervalos é Substituir. Os intervalos definidos são substituídos a partir do principal por Anúncios (O modo de sinalização de anúncio está definido como `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - Nova classe pública que define um único intervalo do `PTTimeRangeCollection`:

   * `property CMTimeRange range` - Define o início e a duração do intervalo.
   * `property long replacementDuration` - Se o tipo de `TimeRangeCollection` é `PTTimeRangeCollectionTypeReplaceRanges`, o `replacementDuration` é usado para criar uma oportunidade de posicionamento (inserção de anúncio) com uma duração de `replacementDuration`. Se a variável `replacementDuration` não estiver definido, o servidor de publicidade determinará a duração e o número de anúncios para essa oportunidade de posicionamento.

* `PTAdSignalingMode`:

   * `PTAdSignalingModeCustomTimeRanges` - Adição de um novo tipo de `PTAdSignalingMode`. Esse modo é usado em conjunto com o `PTTimeRangeCollection` com tipo `PTTimeRangeCollectionReplace` para inserção de anúncio com base nos intervalos de substituição.

* `PTAdMetadata`:

   * `property PTTimeRangeCollection* timeRangeCollection` - Para definir os intervalos de tempo usados nos intervalos de marcação/exclusão/substituição no conteúdo de reprodução.

* Logs de aviso:

   * `UNDEFINED_TIME_RANGES`

      * Tipo - Aviso
      * Descrição - O modo de sinalização de anúncio é definido como intervalos personalizados, mas os intervalos personalizados não são definidos.

   * `INVALID_TIME_RANGES`

      * Tipo - Aviso
      * Descrição - Um ou mais intervalos de tempo são inválidos e serão ignorados ou modificados.

**APIs obsoletas**

* `PTAdMetadata`:

   * `property NSArray* externalAdRanges` - Esta propriedade foi usada anteriormente para definir intervalos C3 para marcação. Agora está obsoleto, pois esses intervalos são definidos via `PTTimeRangeCollection`.
