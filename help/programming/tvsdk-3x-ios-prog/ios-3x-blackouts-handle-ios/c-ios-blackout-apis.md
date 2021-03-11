---
description: O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.
title: Elementos da API de blecaute
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Elementos da API de blecaute {#blackout-api-elements}

O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no reprodutor.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso carregado no momento como o recurso em segundo plano. Se `replaceCurrentItemWithPlayerItem` for chamado após esse método, o TVSDK continuará baixando o manifesto do item de segundo plano até que você chame `unregisterCurrentBackgroundItem` , `stop` ou `reset` .

   * `unregisterCurrentBackgroundItem` Define o item de plano de fundo como nil e para de buscar e analisar o manifesto de plano de fundo.

* **Classe PTMetadata.** PTBlackoutMetadataA  `PTMetadata` específica para blecautes.

   Isso permite que você defina intervalos não pesquisáveis (uma matriz de `CMTimeRanges`) no TVSDK. O TVSDK verifica esses intervalos toda vez que o usuário busca. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK força o visualizador a chegar ao fim do intervalo não pesquisável.

* **INICIE AQUI** **** NEXTPTAdMetadataHabilite ou desabilite o precedente em um stream ao vivo definindo  `enableLivePreroll` como SIM ou NÃO. Se NÃO, o TVSDK não faz uma chamada explícita de servidor de publicidade para anúncios antes da reprodução do conteúdo e, portanto, não reproduz o anúncio precedente. Isso não tem impacto sobre os rolos médios. O padrão é SIM.

* **NSNotifications**

   * `PTTimedMetadataChangedInBackgroundNotification` - Postado quando o TVSDK detecta uma tag inscrita no manifesto em segundo plano e uma nova  `PTTimedMetadata` instância é preparada a partir dela. O objeto da notificação é a instância `PTMediaPlayerItem` que está sendo reproduzida no momento. Você pode buscar a instância `PTTimedMetadata` do dicionário `userInfo` da notificação usando a chave `PTTimedMetadataKey`.

   * `PTBackgroundManifestErrorNotification` - Postado quando o reprodutor de mídia falha completamente ao carregar o manifesto em segundo plano, ou seja, todos os URLs de fluxo retornam um erro ou uma resposta inválida. O objeto da notificação é a instância `PTMediaPlayerItem` que está sendo reproduzida no momento.

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.
   * `INVALID_SEEK_WARNING` Despachado quando uma busca é tentada em um intervalo não pesquisável (em  `nonSeekableRanges` definido em  `PTBlackoutMetadata`).