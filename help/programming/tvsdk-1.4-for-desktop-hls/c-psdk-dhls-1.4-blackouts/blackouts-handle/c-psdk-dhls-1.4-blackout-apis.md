---
description: O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.
title: Elementos da API de blecaute
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Elementos da API de blecaute{#blackout-api-elements}

O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no reprodutor.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso carregado no momento como o recurso em segundo plano. Se `replaceCurrentResource` for chamado após esse método, o TVSDK continuará baixando o manifesto do item de segundo plano até que você chame `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Limpa o recurso em segundo plano definido no momento e para de buscar e analisar o manifesto em segundo plano.

* **** Tipo de metadados BlackoutMetadata que é específico para blecautes.

   Isso permite que você defina intervalos não pesquisáveis (um atributo `TimeRange` adicional chamado `nonseekableRange`) no TVSDK. O TVSDK verifica esses intervalos (se a posição de busca desejada está dentro de um `nonseekableRange`) toda vez que o usuário procura. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK força o visualizador para a hora final do `seekableRange`.

* **INICIE AQUI** **** NEXTDefaultMetadataKeysEnable ou desative a pré-visualização em um stream ao vivo definindo  `ENABLE_LIVE_PREROLL` como true ou false. Se falso, o TVSDK não faz uma chamada explícita de servidor de publicidade para anúncios antes da reprodução do conteúdo e, portanto, não reproduz o anúncio precedente. Isso não tem impacto sobre os rolos médios. O padrão é true.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` subtipo de evento - Despachado quando o TVSDK detecta uma tag subscrita no manifesto em segundo plano.

* **Notificações**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Despachado quando uma busca é tentada em um intervalo não pesquisável.


