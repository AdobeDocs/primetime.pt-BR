---
description: Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.
seo-description: Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.
seo-title: Elementos da API de blecaute
title: Elementos da API de blecaute
uuid: 263a8987-0c85-493a-9352-9605c877ba65
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Elementos da API de blecaute{#blackout-api-elements}

Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.

Quando um blecaute ocorre em um fluxo ao vivo, o player usa manipuladores de eventos para detectar o blecaute e fornecer conteúdo alternativo para os usuários que não têm direito a assistir ao fluxo principal. O player detecta o início e o fim do período de blecaute, altera a reprodução do fluxo principal para um fluxo alternativo e volta para o fluxo principal quando o período de blecaute termina.

Para lidar com blecautes em fluxos ao vivo:

1. Configure seu aplicativo para detectar tags de blecaute assinando tags de blecaute em um manifesto ao vivo.

   O TVSDK não detecta tags de blecaute por si só; você deve assinar as tags de blecaute para receber uma notificação quando as tags forem encontradas durante a análise do arquivo manifest.
1. Crie ouvintes de eventos para tags nas quais o player está inscrito (neste caso, tags PLAYBACK e BLACKOUTS).

   Quando ocorre uma tag à qual o player se inscreveu (por exemplo, uma tag de blecaute) nos manifestos de fluxo de primeiro plano (conteúdo principal) ou de segundo plano (conteúdo alternativo), o TVSDK despacha um `TimedMetadataEvent` e cria um `TimedMetadataObject` para o `TimedMetadataEvent`.

1. Implemente manipuladores para os eventos de metadados cronometrados para os fluxos em primeiro e segundo plano.

   Nesses manipuladores, obtenha as horas de início e fim do período de blecaute dos objetos de evento de metadados cronometrados.
1. Crie métodos para alternar o conteúdo no início e no fim do período de blecaute.

   Quando o período de blecaute começar, alterne o conteúdo principal para o plano de fundo e alterne o conteúdo alternativo para o fluxo principal. Continue buscando e analisando o manifesto original em segundo plano e continuando verificando a tag &quot;blackout end&quot;, para que o player possa ingressar novamente no fluxo original quando o blecaute terminar.
1. Atualize intervalos não pesquisáveis se o intervalo de blecaute estiver em DVR no fluxo de reprodução.

   Rastrear e manipular o fluxo `TimedMetadata` em segundo plano, preparando e atualizando intervalos não pesquisáveis de blecaute.

O TVSDK fornece elementos de API úteis na implementação de blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no player.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso carregado no momento como o recurso em segundo plano. Se `replaceCurrentResource` for chamado após esse método, o TVSDK continuará baixando o manifesto do item em segundo plano até que você chame `unregisterCurrentBackgroundItem`, `release`ou `reset`.

   * `unregisterCurrentBackgroundItem` Define o item de plano de fundo como nulo e para de buscar e analisar o manifesto de plano de fundo.

* **BlackoutMetadata** -

   Uma classe Metadata que é específica para blecautes.

   Isso permite que você defina intervalos não pesquisáveis (uma matriz de `TimeRanges`) no TVSDK. O TVSDK verifica esses intervalos toda vez que o usuário busca. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK força o visualizador a terminar o intervalo não pesquisável.

* **INICIAR AQUI PRÓXIMO AdvertisingMetadata** Ative ou desative a pré-rolagem em um fluxo ao vivo definindo `enableLivePreroll` como true ou false. Se falso, o TVSDK não faz uma chamada explícita do servidor de publicidade para anúncios precedentes antes da reprodução do conteúdo e, portanto, não reproduz o pré-roll. Isso não tem impacto sobre os andares médios. O padrão é verdadeiro.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Despachado quando detecta uma tag assinada no manifesto do plano de fundo e uma nova `TimedMetadata` instância é preparada a partir dela. A `TimedMetadata` instância é despachada como um parâmetro.

   * `onBackgroundManifestFailed` - Despachado quando o player de mídia falha completamente ao carregar o manifesto em segundo plano, ou seja, todos os URLs de fluxo retornam um erro ou uma resposta inválida.

* **Notificações**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.