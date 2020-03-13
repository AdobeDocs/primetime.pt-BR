---
description: O TVSDK fornece elementos de API úteis na implementação de blecautes, incluindo métodos, metadados e notificações.
seo-description: O TVSDK fornece elementos de API úteis na implementação de blecautes, incluindo métodos, metadados e notificações.
seo-title: Elementos da API de blecaute
title: Elementos da API de blecaute
uuid: ddc81558-4218-44d2-92df-15926c7c96b3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Elementos da API de blecaute{#blackout-api-elements}

O TVSDK fornece elementos de API úteis na implementação de blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no player.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso carregado no momento como o recurso em segundo plano. Se `replaceCurrentItemWithPlayerItem` for chamado após esse método, o TVSDK continuará baixando o manifesto do item em segundo plano até que você chame `unregisterCurrentBackgroundItem` , `stop`ou `reset` .

   * `unregisterCurrentBackgroundItem` Define o item de plano de fundo como nulo e para de buscar e analisar o manifesto de plano de fundo.

* **PTMetadata.PTBlackoutMetadata** Uma classe `PTMetadata` específica para blecautes.

   Isso permite que você defina intervalos não pesquisáveis (uma matriz de `CMTimeRanges`) no TVSDK. O TVSDK verifica esses intervalos toda vez que o usuário busca. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK força o visualizador a terminar o intervalo não pesquisável.

* **INICIAR AQUI PRÓXIMO** **PTAdMetadata** Habilite ou desabilite a pré-rolagem em um fluxo ao vivo definindo `enableLivePreroll` como SIM ou NÃO. Se NÃO, o TVSDK não faz uma chamada explícita do servidor de publicidade para anúncios precedentes antes da reprodução do conteúdo e, portanto, não reproduz o pré-roll. Isso não tem impacto sobre os andares médios. O padrão é SIM.

* **NSNotificações**

   * `PTTimedMetadataChangedInBackgroundNotification` - Postado quando o TVSDK detecta uma tag assinada no manifesto do plano de fundo e uma nova `PTTimedMetadata` instância é preparada a partir dele. O objeto da notificação é a `PTMediaPlayerItem` instância que está sendo reproduzida no momento. Você pode buscar a `PTTimedMetadata` instância do `userInfo` dicionário da notificação usando a `PTTimedMetadataKey` chave.

   * `PTBackgroundManifestErrorNotification` - Postado quando o player de mídia falha completamente ao carregar o manifesto em segundo plano, ou seja, todos os URLs de fluxo retornam um erro ou uma resposta inválida. O objeto da notificação é a `PTMediaPlayerItem` instância que está sendo reproduzida no momento.

* **Notificação PTN**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.
   * `INVALID_SEEK_WARNING` Despachado quando uma busca é tentada em um intervalo não pesquisável (em `nonSeekableRanges` definido em `PTBlackoutMetadata`).


