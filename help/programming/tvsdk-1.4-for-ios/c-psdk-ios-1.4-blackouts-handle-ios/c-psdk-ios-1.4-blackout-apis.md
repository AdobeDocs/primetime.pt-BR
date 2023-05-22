---
description: O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.
title: Elementos da API de blecaute
exl-id: 0f098caa-1e2c-4fca-9037-33ebf222021b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Elementos da API de blecaute{#blackout-api-elements}

O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no player.

* **PTMediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso atualmente carregado como o recurso de segundo plano. Se `replaceCurrentItemWithPlayerItem` é chamado após esse método, o TVSDK continua baixando o manifesto do item em segundo plano até que você chame `unregisterCurrentBackgroundItem` , `stop`ou `reset` .

   * `unregisterCurrentBackgroundItem` Define o item de plano de fundo como nil e interrompe a busca e análise do manifesto de plano de fundo.

* **PTMetadata.PTBlackoutMetadata** A `PTMetadata` classe específica para blecautes.

   Isso permite definir intervalos não pesquisáveis (uma matriz de `CMTimeRanges`) no TVSDK. O TVSDK verifica esses intervalos sempre que o usuário busca. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK forçará o visualizador ao final do intervalo não pesquisável.

* **COMECE AQUI EM SEGUIDA** **PTAdMetadata** Ativar ou desativar a pré-rolagem em um stream ao vivo configurando `enableLivePreroll` para SIM ou NÃO. Se NÃO, o TVSDK não faz uma chamada explícita do servidor de anúncios para anúncios precedentes à reprodução do conteúdo e, portanto, não reproduz os anúncios precedentes. Isso não afeta os rolos intermediários. O padrão é SIM.

* **Notificações NSN**

   * `PTTimedMetadataChangedInBackgroundNotification` - Publicado quando o TVSDK detecta uma tag inscrita no manifesto em segundo plano e um novo `PTTimedMetadata` instância é preparada a partir dela. O objeto da notificação é o `PTMediaPlayerItem` instância que está sendo executada no momento. Você pode buscar o `PTTimedMetadata` instância da notificação `userInfo` usando o `PTTimedMetadataKey` chave.

   * `PTBackgroundManifestErrorNotification` - Publicado quando o reprodutor de mídia falha completamente ao carregar o manifesto em segundo plano, ou seja, todos os URLs de fluxo retornam um erro ou uma resposta inválida. O objeto da notificação é o `PTMediaPlayerItem` instância que está sendo executada no momento.

* **PTNotification**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.
   * `INVALID_SEEK_WARNING` Despachado quando uma busca é tentada em um intervalo não pesquisável (em `nonSeekableRanges` definido em `PTBlackoutMetadata`).
