---
description: Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.
seo-description: Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.
seo-title: Trabalhar com blecautes em fluxos ao vivo
title: Trabalhar com blecautes em fluxos ao vivo
uuid: df933087-c8a8-49eb-a016-6dfd971c219c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# Gerenciar blecautes em fluxos ao vivo{#handle-blackouts-in-live-streams}

Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.

Quando um blecaute ocorre em um fluxo ao vivo, o player usa manipuladores de evento para detectar o blecaute e fornecer conteúdo alternativo para os usuários que não têm direito a assistir ao fluxo principal. O player detecta o start e o fim do período de blecaute, alterna a reprodução do fluxo principal para um fluxo alternativo e volta para o fluxo principal quando o período de blecaute termina.

No aplicativo cliente, você assina tags de blecaute no TVSDK. Ao ser notificado sobre novos objetos *metadados cronometrados*, você analisa os dados do objeto de metadados cronometrados para identificar se o objeto indica uma entrada ou saída de blecaute. Para blecautes identificados, você chama os elementos relevantes do TVSDK para alternar para conteúdo alternativo no início do blecaute e, novamente, para voltar ao conteúdo principal quando o blecaute terminar.

>[!TIP]
>
>As teclas ainda são baixadas do manifesto antes que o conteúdo seja reproduzido.

Quando um usuário se conecta a um fluxo ao vivo depois que o período de blecaute termina e rola de volta no tempo para o período de blecaute, o conteúdo será reproduzido.

>[!IMPORTANT]
>
>Se todas as solicitações de chave falharem, um erro será emitido ao analisar o manifesto. Se algumas solicitações falharem e algumas tiverem êxito, o TVSDK tentará reproduzir o conteúdo. Se o TVSDK tentar reproduzir uma seção do conteúdo, mas não houver uma chave válida para descriptografar esse conteúdo, ele retornará um erro.

Para lidar com blecautes em fluxos ao vivo:

1. Configure seu aplicativo para detectar tags de blecaute assinando tags de blecaute em um manifesto ao vivo.

   O TVSDK não detecta tags de blecaute por si só; você deve assinar as tags de blecaute para receber uma notificação quando as tags forem encontradas durante a análise do arquivo manifest.
1. Crie ouvintes de evento para tags nas quais o player está inscrito.

   Quando ocorre uma tag à qual o player se inscreveu (por exemplo, uma tag de blecaute) nos manifestos de fluxo em primeiro plano (conteúdo principal) ou em segundo plano (conteúdo alternativo), o TVSDK despacha um `TimedMetadataEvent` e cria um `TimedMetadataObject` para o `TimedMetadataEvent`.
1. Implemente manipuladores para os eventos de metadados cronometrados para os fluxos em primeiro e segundo plano.

   Nesses manipuladores, obtenha o start e as horas de término do período de blecaute dos objetos de evento de metadados cronometrados.
1. Prepare o `MediaPlayer` para blecautes.

   Quando `MediaPlayer` entrar no estado PREPARADO, você calcula e prepara os intervalos de blecaute e os define no objeto `MediaPlayer`.

1. Para cada atualização na posição do indicador de reprodução, verifique a lista de `TimedMetadataObjects`.

   Este é o local onde o player detecta o start de blecaute e termina, e rastreia o tempo do blecaute como ele ocorre.

1. Crie métodos para alternar o conteúdo no start e no final do período de blecaute.

   Quando o período de blecaute start, alterne o conteúdo principal para o plano de fundo e alterne o conteúdo alternativo para o fluxo principal. Continue buscando e analisando o manifesto original em segundo plano e continuando verificando a tag &quot;blackout end&quot;, para que o player possa ingressar novamente no fluxo original quando o blecaute terminar.

