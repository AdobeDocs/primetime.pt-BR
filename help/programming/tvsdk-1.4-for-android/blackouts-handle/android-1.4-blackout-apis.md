---
description: Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.
title: Elementos da API de blecaute
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# Elementos da API de blecaute{#blackout-api-elements}

Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.

Quando um blecaute ocorre em um stream ao vivo, o player usa manipuladores de eventos para detectar o blecaute e fornecer conteúdo alternativo para os usuários não qualificados para assistir ao stream principal. O reprodutor detecta o início e o fim do período de blecaute, alterna a reprodução do fluxo principal para um fluxo alternativo e retorna ao fluxo principal quando o período de blecaute termina.

Para lidar com blecautes em fluxos ao vivo:

1. Configure seu aplicativo para detectar tags de blecaute, assinando tags de blecaute em um manifesto live-stream.

   O TVSDK não detecta tags de blecaute por conta própria; você deve assinar tags de blecaute para receber notificação quando as tags forem encontradas durante a análise do arquivo de manifesto.
1. Crie ouvintes de eventos para tags nas quais seu reprodutor está inscrito (neste caso, tags PLAYBACK e BLACKOUTS ).

   Quando ocorre uma tag na qual o reprodutor se inscreveu (por exemplo, uma tag de blecaute) nos manifestos de primeiro plano (conteúdo principal) ou de segundo plano (conteúdo alternativo), o TVSDK despacha um `TimedMetadataEvent` e cria um `TimedMetadataObject` para o `TimedMetadataEvent`.

1. Implemente manipuladores para os eventos de metadados cronometrados para os fluxos de primeiro e segundo plano.

   Nesses manipuladores, obtenha as horas de início e término do período de blecaute a partir dos objetos de evento de metadados cronometrados.
1. Crie métodos para alternar o conteúdo no início e no fim do período de blecaute.

   Quando o período de blecaute começar, alterne o conteúdo principal para o plano de fundo e alterne o conteúdo alternativo para o fluxo principal. Continue a buscar e analisar o manifesto original em segundo plano e a verificar a tag &quot;blackout end&quot; para que o reprodutor possa ingressar novamente no fluxo original quando o blackout terminar.
1. Atualize intervalos não pesquisáveis se o intervalo de blecaute estiver em DVR no fluxo de reprodução.

   Rastreie e manipule o `TimedMetadata` no fluxo de fundo, preparando e atualizando intervalos não pesquisáveis com blecaute.

O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no reprodutor.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso carregado no momento como o recurso em segundo plano. Se `replaceCurrentResource` for chamado após esse método, o TVSDK continuará baixando o manifesto do item de plano de fundo até que você chame `unregisterCurrentBackgroundItem`, `release` ou `reset`.

   * `unregisterCurrentBackgroundItem` Define o item de plano de fundo como nulo e para de buscar e analisar o manifesto de plano de fundo.

* **BlackoutMetadata**  -

   Uma classe de Metadados específica para blecautes.

   Isso permite que você defina intervalos não pesquisáveis (uma matriz de `TimeRanges`) no TVSDK. O TVSDK verifica esses intervalos toda vez que o usuário busca. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK força o visualizador a chegar ao fim do intervalo não pesquisável.

* **INICIE AQUI PRÓXIMO** AdvertisingMetadataEnable ou desative o pré-lançamento em um stream ao vivo definindo  `enableLivePreroll` como verdadeiro ou falso. Se falso, o TVSDK não faz uma chamada explícita de servidor de publicidade para anúncios antes da reprodução do conteúdo e, portanto, não reproduz o anúncio precedente. Isso não tem impacto sobre os rolos médios. O padrão é true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Despachado quando detecta uma tag inscrita no manifesto em segundo plano e uma nova  `TimedMetadata` instância é preparada a partir dela. A instância `TimedMetadata` é despachada como um parâmetro.

   * `onBackgroundManifestFailed` - Despachado quando o reprodutor de mídia falha completamente ao carregar o manifesto em segundo plano, ou seja, todos os URLs de fluxo retornam um erro ou uma resposta inválida.

* **Notificações**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.