---
description: Eventos e notificações ajudam a gerenciar os aspectos assíncronos do aplicativo de vídeo.
seo-description: Eventos e notificações ajudam a gerenciar os aspectos assíncronos do aplicativo de vídeo.
seo-title: Notificações e eventos para status, atividade, erros e registro do player
title: Notificações e eventos para status, atividade, erros e registro do player
uuid: c4a108e7-72aa-4c96-9538-b1385343d6af
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Notificações e eventos para status, atividade, erros e registro do player {#notifications-and-events-for-player-status-activity-errors-and-logging}

Eventos e notificações ajudam a gerenciar os aspectos assíncronos do aplicativo de vídeo.

`MediaPlayerStatus` objetos fornecem informações sobre alterações no status do player. `Notification` objetos fornecem informações sobre avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player. Você implementa ouvintes de eventos para capturar e responder a eventos ( `MediaPlayerEvent` objetos).

Seu aplicativo pode recuperar informações de notificação e status. Usando essas informações, você também pode criar um sistema de registro para diagnóstico e validação.

## Conteúdo da notificação {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` fornece informações relacionadas ao status do player.

O TVSDK fornece uma lista cronológica de `MediaPlayerNotification` notificações e cada notificação contém as seguintes informações:

* Um carimbo de data e hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFO, AVISO ou ERRO.
   * `code`: Uma representação numérica da notificação.
   * `name`: Uma descrição legível pela pessoa da notificação, como SEEK_ERROR
   * `metadata`: Pares chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outro `MediaPlayerNotification` objeto que afeta diretamente essa notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las para um servidor remoto para registro e representação gráfica.

## Configurar seu sistema de notificação {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Você pode acompanhar as notificações.

O núcleo do sistema de notificação do Primetime Player é a `Notification` classe, que representa uma notificação independente.

Para receber notificações, ouça as notificações da seguinte maneira:

1. Implemente o `NotificationEventListener.onNotification()` retorno de chamada.
1. O TVSDK passa um `NotificationEvent` objeto para o retorno de chamada.

   >[!NOTE]
   >
   >Os tipos de notificações são enumerados na `Notification.Type` enumeração:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Adicionar registro e depuração em tempo real {#section_9D4004308CB243AD9B50818895D10005}

Você pode usar notificações para implementar o logon em tempo real no aplicativo de vídeo.

O sistema de notificação permite coletar informações de registro e depuração para diagnóstico e validação sem estressar o sistema.

>[!IMPORTANT]
>
>O back-end de logon não faz parte de uma configuração de produção e não é esperado que trate de tráfego de alta carga. Se sua implementação não precisar ser totalmente concluída, considere a eficiência da transmissão de dados para evitar sobrecarregar seu sistema.

Este é um exemplo de como recuperar notificações:

1. Crie um thread de execução com base em temporizador para seu aplicativo de vídeo que consulta periodicamente os dados coletados pelo sistema de notificação TVSDK.
1. Se o intervalo do temporizador for muito grande e o tamanho da lista de eventos for muito pequeno, a lista de eventos de notificação será estendida.

   >[!NOTE]
   >
   >Para evitar esse sobrefluxo, execute um dos procedimentos a seguir:    >
   >    
   >    
   >    1. Diminua o intervalo de tempo que direciona o thread que pesquisa novos eventos.
   >    1. Aumente o tamanho da lista de notificações.


1. Serialize as entradas de evento de notificação mais recentes no formato JSON e envie as entradas para um servidor remoto para pós-processamento.

   >[!NOTE]
   >
   >O servidor remoto pode exibir graficamente os dados fornecidos em tempo real.

1. Para detectar a perda de eventos de notificação, procure por lacunas na sequência de valores de índice de eventos.