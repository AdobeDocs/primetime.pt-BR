---
description: Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.
title: Gerenciar blecautes em fluxos dinâmicos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Gerenciar blecautes em fluxos ao vivo{#handle-blackouts-in-live-streams}

Você pode lidar com blecautes em fluxos de vídeo ao vivo e fornecer conteúdo alternativo durante um blecaute.

Quando um blecaute ocorre em um stream ao vivo, o player usa manipuladores de eventos para detectar o blecaute e fornecer conteúdo alternativo para os usuários não qualificados para assistir ao stream principal. O reprodutor detecta o início e o fim do período de blecaute, alterna a reprodução do fluxo principal para um fluxo alternativo e retorna ao fluxo principal quando o período de blecaute termina.

No aplicativo cliente, você assina tags de blecaute no TVSDK. Após ser notificado sobre novos objetos de *metadados cronometrados*, você analisa os dados do objeto de metadados cronometrados para identificar se o objeto indica uma entrada ou saída de blecaute. Para blecautes identificados, você chama os elementos relevantes do TVSDK para alternar para o conteúdo alternativo no início do blecaute e, novamente, para retornar ao conteúdo principal quando o blecaute terminar.

>[!TIP]
>
>As chaves ainda são baixadas do manifesto antes da reprodução do conteúdo.

Quando um usuário se conecta a um stream ao vivo após o término do período de blecaute e rola de volta no tempo para o período de blecaute, o conteúdo será reproduzido.

>[!IMPORTANT]
>
>Se todas as solicitações principais falharem, um erro será lançado ao analisar o manifesto. Se algumas solicitações falharem e algumas forem bem-sucedidas, o TVSDK tentará reproduzir o conteúdo. Se o TVSDK tentar reproduzir uma seção do conteúdo, mas não houver uma chave válida para descriptografar esse conteúdo, ele retornará um erro.

Para lidar com blecautes em fluxos ao vivo:

1. Configure seu aplicativo para detectar tags de blecaute, assinando tags de blecaute em um manifesto live-stream.

   O TVSDK não detecta tags de blecaute por conta própria; você deve assinar tags de blecaute para receber notificação quando as tags forem encontradas durante a análise do arquivo de manifesto.
1. Crie ouvintes de eventos para tags nas quais o reprodutor é inscrito.

   Quando ocorre uma tag na qual o reprodutor se inscreveu (por exemplo, uma tag de blecaute) nos manifestos de primeiro plano (conteúdo principal) ou de segundo plano (conteúdo alternativo), o TVSDK despacha um `TimedMetadataEvent` e cria um `TimedMetadataObject` para o `TimedMetadataEvent`.
1. Implemente manipuladores para os eventos de metadados cronometrados para os fluxos de primeiro e segundo plano.

   Nesses manipuladores, obtenha as horas de início e término do período de blecaute a partir dos objetos de evento de metadados cronometrados.
1. Prepare o `MediaPlayer` para blecautes.

   Quando o `MediaPlayer` entrar no estado PREPARADO, você calcula e prepara os intervalos de blecaute e os define no objeto `MediaPlayer`.

1. Para cada atualização na posição do indicador de reprodução, verifique a lista de `TimedMetadataObjects`.

   É aqui que o reprodutor detecta o início e o fim do blecaute e rastreia o tempo do blecaute como ele ocorre.

1. Crie métodos para alternar o conteúdo no início e no fim do período de blecaute.

   Quando o período de blecaute começar, alterne o conteúdo principal para o plano de fundo e alterne o conteúdo alternativo para o fluxo principal. Continue a buscar e analisar o manifesto original em segundo plano e a verificar a tag &quot;blackout end&quot; para que o reprodutor possa ingressar novamente no fluxo original quando o blackout terminar.

