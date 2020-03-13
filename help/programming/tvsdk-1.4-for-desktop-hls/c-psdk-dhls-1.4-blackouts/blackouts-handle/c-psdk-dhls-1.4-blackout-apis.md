---
description: O TVSDK fornece elementos de API úteis na implementação de blecautes, incluindo métodos, metadados e notificações.
seo-description: O TVSDK fornece elementos de API úteis na implementação de blecautes, incluindo métodos, metadados e notificações.
seo-title: Elementos da API de blecaute
title: Elementos da API de blecaute
uuid: 65e1668c-6a19-4910-83a2-46d364e94e5f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Elementos da API de blecaute{#blackout-api-elements}

O TVSDK fornece elementos de API úteis na implementação de blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no player.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso carregado no momento como o recurso em segundo plano. Se `replaceCurrentResource` for chamado após esse método, o TVSDK continuará baixando o manifesto do item em segundo plano até que você chame `unregisterCurrentBackgroundItem`.

   * `unregisterCurrentBackgroundItem`  Limpa o recurso em segundo plano definido no momento e para de buscar e analisar o manifesto em segundo plano.

* **BlackoutMetadata** Um tipo de Metadados que é específico para blecautes.

   Isso permite definir intervalos não pesquisáveis (um `TimeRange` atributo adicional chamado `nonseekableRange`) no TVSDK. O TVSDK verifica esses intervalos (se a posição de busca desejada está dentro de uma `nonseekableRange`) toda vez que o usuário busca. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK força o visualizador para a hora de término do `seekableRange`.

* **INICIAR AQUI PRÓXIMO** **DefaultMetadataKeys** Ative ou desative a pré-rolagem em um fluxo ao vivo definindo `ENABLE_LIVE_PREROLL` como true ou false. Se falso, o TVSDK não faz uma chamada explícita do servidor de publicidade para anúncios precedentes antes da reprodução do conteúdo e, portanto, não reproduz o pré-roll. Isso não tem impacto sobre os andares médios. O padrão é verdadeiro.

* **TimedMetadataEvent**

   * `TIMED_METADATA_IN_BACKGROUND_AVAILABLE` subtipo de evento - Despachado quando o TVSDK detecta uma tag subscrita no manifesto em segundo plano.

* **Notificações**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` Despachado quando uma busca é tentada em um intervalo não pesquisável.


