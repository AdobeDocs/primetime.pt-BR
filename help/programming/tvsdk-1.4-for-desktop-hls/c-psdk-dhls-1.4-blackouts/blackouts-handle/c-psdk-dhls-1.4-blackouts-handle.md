---
description: Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.
title: Lidar com blecautes em fluxos ao vivo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Lidar com blecautes em fluxos ao vivo{#handle-blackouts-in-live-streams}

Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.

Quando um blecaute ocorre em um stream ao vivo, o reprodutor usa manipuladores de eventos para detectar o blecaute e fornecer conteúdo alternativo aos usuários que não são elegíveis para assistir ao stream principal. O reprodutor detecta o início e o fim do período de blecaute, alterna a reprodução do fluxo principal para um fluxo alternativo e retorna ao fluxo principal quando o período de blecaute termina.

No aplicativo cliente, você assina tags de blecaute no TVSDK. Ao ser notificado de novas *metadados cronometrados* objetos, você analisa os dados do objeto de metadados cronometrados para identificar se o objeto indica uma entrada ou saída de blecaute. Para blecautes identificados, você chama os elementos TVSDK relevantes para alternar para o conteúdo alternativo no início do blecaute e novamente para retornar ao conteúdo principal quando o blecaute terminar.

>[!TIP]
>
>As chaves ainda são baixadas do manifesto antes que o conteúdo seja reproduzido.

Quando um usuário se conecta a um fluxo ao vivo após o término do período de blecaute e rola de volta no tempo para o período de blecaute, o conteúdo é reproduzido.

>[!IMPORTANT]
>
>Se todas as solicitações de chave falharem, um erro será lançado ao analisar o manifesto. Se algumas solicitações falharem e algumas forem bem-sucedidas, o TVSDK tentará reproduzir o conteúdo. Se o TVSDK tentar reproduzir uma seção do conteúdo, mas não houver uma chave válida para descriptografar esse conteúdo, retornará um erro.

Para lidar com blecautes em fluxos ao vivo:

1. Configure seu aplicativo para detectar tags de blecaute inscrevendo-se em tags de blecaute em um manifesto em tempo real.

   O TVSDK não detecta tags de blecaute por conta própria; você deve assinar tags de blecaute para receber notificação quando as tags forem encontradas durante a análise do arquivo de manifesto.
1. Crie ouvintes de eventos para as tags às quais o player está inscrito.

   Quando ocorre uma tag na qual o player está inscrito (por exemplo, uma tag de blecaute) nos manifestos de fluxo em primeiro ou segundo plano (conteúdo alternativo), o TVSDK envia um `TimedMetadataEvent` e cria um `TimedMetadataObject` para o `TimedMetadataEvent`.
1. Implemente manipuladores para os eventos de metadados cronometrados para os fluxos de primeiro e segundo plano.

   Nesses manipuladores, obtenha as horas de início e término do período de blecaute a partir dos objetos de evento de metadados cronometrados.
1. Prepare o `MediaPlayer` para blecautes.

   Quando a variável `MediaPlayer` entra no estado PREPARED, você calcula e prepara os intervalos de blecaute e os define no estado `MediaPlayer` objeto.

1. Para cada atualização na posição do indicador de reprodução, verifique a lista de `TimedMetadataObjects`.

   É aqui que o player detecta o início e o término do blecaute e rastreia o tempo do blecaute à medida que ele ocorre.

1. Crie métodos para alternar o conteúdo no início e no fim do período de blecaute.

   Quando o período de blecaute começar, alterne o conteúdo principal para o plano de fundo e alterne o conteúdo alternativo para se tornar o fluxo principal. Continue a buscar e analisar o manifesto original em segundo plano e continue verificando a tag &quot;blackout end&quot;, para que o reprodutor possa reingressar no fluxo original quando o blecaute terminar.
