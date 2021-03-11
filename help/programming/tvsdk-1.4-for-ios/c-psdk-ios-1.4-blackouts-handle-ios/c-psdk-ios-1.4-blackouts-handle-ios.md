---
description: O TVSDK lida com blecautes em fluxos de vídeo ao vivo e fornece conteúdo alternativo durante um blecaute.
title: Gerenciar blecautes em fluxos dinâmicos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Gerenciar blecautes em fluxos ao vivo{#handle-blackouts-in-live-streams}

O TVSDK lida com blecautes em fluxos de vídeo ao vivo e fornece conteúdo alternativo durante um blecaute.

O caso de uso mais comum associado a um blecaute de programação é quando o aplicativo do reprodutor fornece conteúdo alternativo para usuários não qualificados para assistir ao stream principal. Este aplicativo pode usar o TVSDK para determinar o início e o fim do período de blecaute. Dessa forma, no início do período de blecaute, a reprodução pode alternar do fluxo principal para um fluxo alternativo e, em seguida, alternar de volta para o fluxo principal quando o período de blecaute terminar.

Para implementar a solução para este caso de uso:

1. Configure seu aplicativo para assinar tags de blecaute em um manifesto de fluxo ao vivo.

   O TVSDK não está ciente diretamente das tags de blecaute, mas permite que seu aplicativo se inscreva em notificações quando tags específicas forem encontradas durante a análise do arquivo de manifesto.
1. Adicione um ouvinte de notificação para `PTTimedMetadataChangedNotification`.

   Essa notificação é despachada sempre que uma tag subscrita é analisada no manifesto e um novo `PTTimedMetadata` é preparado a partir dele.

1. Implemente um método de ouvinte, como `onMediaPlayerSubscribedTagIdentified`, para objetos `PTTimedMetadata` em primeiro plano.

1. Sempre que houver uma atualização durante a reprodução, use o ouvinte `PTMediaPlayerTimeChangeNotification` para manipular objetos `PTTimedMetadata`.

1. Adicione o manipulador `PTTimedMetadata`.

   Esse manipulador permite alternar para o conteúdo alternativo e retornar ao conteúdo principal, conforme indicado pelo objeto `PTTimedMetadata` e seu tempo de reprodução.

1. Use `onSubscribedTagInBackground` para implementar o método de ouvinte para objetos `PTTimedMetadata` em segundo plano.

   Esse método monitora o tempo no fluxo em segundo plano, o que ajuda a determinar quando você pode alternar de conteúdo alternativo para conteúdo principal.

1. Implemente um método listener para erros em segundo plano.
1. Se o intervalo de blecaute estiver no DVR no fluxo de reprodução, atualize os intervalos não pesquisáveis.

   O aplicativo deve definir o intervalo não pesquisável no DVR nos seguintes casos:

   * Ao entrar no fluxo principal quando um blecaute estiver no DVR.
   * Ao retornar ao conteúdo principal do conteúdo alternativo.

