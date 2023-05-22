---
description: O TVSDK lida com blecautes em fluxos de vídeo ao vivo e fornece conteúdo alternativo durante um blecaute.
title: Lidar com blecautes em fluxos ao vivo
exl-id: 772700ac-2b6d-4bf9-9400-c357dd77f701
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Lidar com blecautes em fluxos ao vivo{#handle-blackouts-in-live-streams}

O TVSDK lida com blecautes em fluxos de vídeo ao vivo e fornece conteúdo alternativo durante um blecaute.

O caso de uso mais comum associado a um blecaute de programação é quando seu aplicativo player fornece conteúdo alternativo para usuários que não estão qualificados para assistir ao fluxo principal. Este aplicativo pode usar o TVSDK para determinar o início e o fim do período de blecaute. Dessa forma, no início do período de blecaute, a reprodução pode alternar do fluxo principal para um fluxo alternativo e, em seguida, alternar de volta para o fluxo principal quando o período de blecaute terminar.

Para implementar a solução para este caso de uso:

1. Configure seu aplicativo para assinar tags de blecaute em um manifesto de transmissão ao vivo.

   O TVSDK não tem conhecimento direto das tags de blecaute, mas permite que seu aplicativo assine notificações quando tags específicas são encontradas durante a análise do arquivo de manifesto.
1. Adicionar um ouvinte de notificação para `PTTimedMetadataChangedNotification`.

   Essa notificação é despachada sempre que uma tag assinada é analisada no manifesto e uma nova `PTTimedMetadata` é preparado a partir dele.

1. Implementar um método de ouvinte, como `onMediaPlayerSubscribedTagIdentified`, para `PTTimedMetadata` objetos em primeiro plano.

1. Cada vez que houver uma atualização durante a reprodução, use o `PTMediaPlayerTimeChangeNotification` ouvinte a ser manipulado `PTTimedMetadata` objetos.

1. Adicione o `PTTimedMetadata` manipulador.

   Esse manipulador permite alternar para um conteúdo alternativo e retornar ao conteúdo principal conforme indicado pela `PTTimedMetadata` objeto e seu tempo de reprodução.

1. Uso `onSubscribedTagInBackground` para implementar o método listener para `PTTimedMetadata` objetos em segundo plano.

   Esse método monitora o tempo no fluxo em segundo plano, o que ajuda a determinar quando é possível alternar do conteúdo alternativo de volta para o conteúdo principal.

1. Implemente um método de ouvinte para erros em segundo plano.
1. Se o intervalo de blecaute estiver no DVR no fluxo de reprodução, atualize os intervalos não pesquisáveis.

   Seu aplicativo deve definir o intervalo não pesquisável no DVR nos seguintes casos:

   * Ao ingressar no fluxo principal quando um blecaute estiver no DVR.
   * Ao voltar para o conteúdo principal do conteúdo alternativo.
