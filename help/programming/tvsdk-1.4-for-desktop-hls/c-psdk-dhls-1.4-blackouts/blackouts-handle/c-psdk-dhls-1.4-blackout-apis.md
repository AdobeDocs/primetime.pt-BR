---
description: O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.
title: Elementos da API de blecaute
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Elementos da API de blecaute{#blackout-api-elements}

O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no player.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso atualmente carregado como o recurso de segundo plano. Se `replaceCurrentResource` é chamado após esse método, o TVSDK continua baixando o manifesto do item em segundo plano até que você chame `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Limpa o recurso de segundo plano definido no momento e interrompe a busca e análise do manifesto de segundo plano.

* **BlackoutMetadata** Um tipo de Metadados específico para blecautes.

  Isso permite que você defina intervalos não pesquisáveis (um intervalo `TimeRange` atributo chamado `nonseekableRange`) no TVSDK. O TVSDK verifica esses intervalos (se a posição de busca desejada se enquadra em um `nonseekableRange`) sempre que o usuário buscar. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK forçará o visualizador a encerrar a hora do `seekableRange`.

* **COMECE AQUI EM SEGUIDA** **DefaultMetadataKeys** Ativar ou desativar a pré-rolagem em um stream ao vivo configurando `ENABLE_LIVE_PREROLL` para verdadeiro ou falso. Se for falso, o TVSDK não fará uma chamada explícita do servidor de anúncios para anúncios precedentes à reprodução do conteúdo e, portanto, não reproduzirá o anúncio anterior à reprodução. Isso não afeta os rolos intermediários. O padrão é true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` subtipo de evento - Despachado quando o TVSDK detecta uma tag inscrita no manifesto em segundo plano.

* **Notificação**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.

   * `SeekEvent.SEEK_POSITION_ADJUSTED` Despachado quando uma busca é tentada em um intervalo não pesquisável.
