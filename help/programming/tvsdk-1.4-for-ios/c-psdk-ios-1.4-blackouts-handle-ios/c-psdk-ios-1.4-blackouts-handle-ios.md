---
description: O TVSDK trata de blecautes em fluxos de vídeo ao vivo e fornece conteúdo alternativo durante um blecaute.
seo-description: O TVSDK trata de blecautes em fluxos de vídeo ao vivo e fornece conteúdo alternativo durante um blecaute.
seo-title: Trabalhar com blecautes em fluxos ao vivo
title: Trabalhar com blecautes em fluxos ao vivo
uuid: 1f70a272-bc77-4d41-a999-b076cb42ac5e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Gerenciar blecautes em fluxos ao vivo{#handle-blackouts-in-live-streams}

O TVSDK trata de blecautes em fluxos de vídeo ao vivo e fornece conteúdo alternativo durante um blecaute.

O caso de uso mais comum associado a um blecaute de programação é quando o aplicativo do player fornece conteúdo alternativo para usuários não qualificados para assistir ao fluxo principal. Este aplicativo pode usar o TVSDK para determinar o início e o fim do período de blecaute. Dessa forma, no início do período de blecaute, a reprodução pode alternar do fluxo principal para um fluxo alternativo e, em seguida, alternar de volta para o fluxo principal quando o período de blecaute terminar.

Para implementar a solução para este caso de uso:

1. Configure seu aplicativo para assinar tags de blecaute em um manifesto de fluxo ao vivo.

   O TVSDK não está ciente diretamente das tags de blecaute, mas permite que seu aplicativo assine notificações quando tags específicas forem encontradas durante a análise do arquivo manifest.
1. Adicione um ouvinte de notificação para `PTTimedMetadataChangedNotification`.

   Esta notificação é enviada sempre que uma tag assinada é analisada no manifesto e um novo `PTTimedMetadata` é preparado a partir dele.

1. Implemente um método de ouvinte, como `onMediaPlayerSubscribedTagIdentified`, para objetos `PTTimedMetadata` em primeiro plano.

1. Sempre que houver uma atualização durante a reprodução, use o ouvinte `PTMediaPlayerTimeChangeNotification` para manipular os objetos `PTTimedMetadata`.

1. Adicione o manipulador `PTTimedMetadata`.

   Esse manipulador permite alternar para o conteúdo alternativo e retornar ao conteúdo principal, conforme indicado pelo objeto `PTTimedMetadata` e seu tempo de reprodução.

1. Use `onSubscribedTagInBackground` para implementar o método listener para objetos `PTTimedMetadata` em segundo plano.

   Este método monitora a temporização no fluxo em segundo plano, o que ajuda a determinar quando você pode alternar de conteúdo alternativo de volta para o conteúdo principal.

1. Implemente um método de escuta para erros em segundo plano.
1. Se o intervalo de blecaute estiver no DVR no fluxo de reprodução, atualize os intervalos não pesquisáveis.

   Seu aplicativo deve definir o intervalo não pesquisável no DVR nos seguintes casos:

   * Quando entrar no fluxo principal quando um blecaute estiver no DVR.
   * Ao voltar para o conteúdo principal a partir do conteúdo alternativo.

