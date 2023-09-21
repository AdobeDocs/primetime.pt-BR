---
description: Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.
title: Elementos da API de blecaute
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Elementos da API de blecaute{#blackout-api-elements}

Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.

Quando um blecaute ocorre em um stream ao vivo, o reprodutor usa manipuladores de eventos para detectar o blecaute e fornecer conteúdo alternativo aos usuários que não são elegíveis para assistir ao stream principal. O reprodutor detecta o início e o fim do período de blecaute, alterna a reprodução do fluxo principal para um fluxo alternativo e retorna ao fluxo principal quando o período de blecaute termina.

Para lidar com blecautes em fluxos ao vivo:

1. Configure seu aplicativo para detectar tags de blecaute inscrevendo-se em tags de blecaute em um manifesto em tempo real.

   O TVSDK não detecta tags de blecaute por conta própria; você deve assinar tags de blecaute para receber notificação quando as tags forem encontradas durante a análise do arquivo de manifesto.
1. Crie ouvintes de eventos para tags nas quais o player está inscrito (nesse caso, tags PLAYBACK e BLACKOUTS ).

   Quando ocorre uma tag na qual o player está inscrito (por exemplo, uma tag de blecaute) nos manifestos de fluxo em primeiro ou segundo plano (conteúdo alternativo), o TVSDK envia um `TimedMetadataEvent` e cria um `TimedMetadataObject` para o `TimedMetadataEvent`.

1. Implemente manipuladores para os eventos de metadados cronometrados para os fluxos de primeiro e segundo plano.

   Nesses manipuladores, obtenha as horas de início e término do período de blecaute a partir dos objetos de evento de metadados cronometrados.
1. Crie métodos para alternar o conteúdo no início e no fim do período de blecaute.

   Quando o período de blecaute começar, alterne o conteúdo principal para o plano de fundo e alterne o conteúdo alternativo para se tornar o fluxo principal. Continue a buscar e analisar o manifesto original em segundo plano e continue verificando a tag &quot;blackout end&quot;, para que o reprodutor possa reingressar no fluxo original quando o blecaute terminar.
1. Atualize intervalos não pesquisáveis se o intervalo de blecaute estiver em DVR no fluxo de reprodução.

   Rastrear e manipular o `TimedMetadata` no fluxo em segundo plano, preparando e atualizando intervalos não pesquisáveis de blecaute.

O TVSDK fornece elementos de API úteis ao implementar blecautes, incluindo métodos, metadados e notificações.

Você pode usar o seguinte ao implementar uma solução de blecaute no player.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Salva o recurso atualmente carregado como o recurso de segundo plano. Se `replaceCurrentResource` é chamado após esse método, o TVSDK continua baixando o manifesto do item em segundo plano até que você chame `unregisterCurrentBackgroundItem`, `release`ou `reset`.

   * `unregisterCurrentBackgroundItem` Define o item de plano de fundo como nulo e interrompe a busca e análise do manifesto de plano de fundo.

* **BlackoutMetadata** -

  Uma classe de Metadados específica para blecautes.

  Isso permite definir intervalos não pesquisáveis (uma matriz de `TimeRanges`) no TVSDK. O TVSDK verifica esses intervalos sempre que o usuário busca. Se estiver definido e o usuário buscar em um intervalo não pesquisável, o TVSDK forçará o visualizador ao final do intervalo não pesquisável.

* **COMECE AQUI PRÓXIMO AdvertisingMetadata** Ativar ou desativar a pré-rolagem em um stream ao vivo configurando `enableLivePreroll` para verdadeiro ou falso. Se for falso, o TVSDK não fará uma chamada explícita do servidor de anúncios para anúncios precedentes à reprodução do conteúdo e, portanto, não reproduzirá o anúncio anterior à reprodução. Isso não afeta os rolos intermediários. O padrão é true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Despachado quando o detecta uma tag inscrita no manifesto em segundo plano e uma nova `TimedMetadata` instância é preparada a partir dela. A variável `TimedMetadata` é despachada como um parâmetro.

   * `onBackgroundManifestFailed` - Despachado quando o reprodutor de mídia falha completamente ao carregar o manifesto em segundo plano, ou seja, todos os URLs de fluxo retornam um erro ou uma resposta inválida.

* **Notificação**

   * `BACKGROUND_MANIFEST_WARNING`

      * Código: 204000
      * Tipo: Aviso
      * Erro no download do manifesto em segundo plano.
