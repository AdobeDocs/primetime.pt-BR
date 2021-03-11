---
description: Os objetos MediaPlayerStatus fornecem informações sobre alterações no status do player. Os objetos de notificação fornecem informações sobre avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor. Você implementa ouvintes de eventos para capturar e responder a eventos (objetos MediaPlayerEvent ).
title: Notificações e eventos para status, atividade, erros e registro do player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Notificações e eventos para status do player, atividade, erros e registro {#notifications-and-events-for-player-status-activity-errors-and-logging}

Eventos e notificações ajudam você a gerenciar os aspectos assíncronos do aplicativo de vídeo.

Os objetos MediaPlayerStatus fornecem informações sobre alterações no status do player. Os objetos de notificação fornecem informações sobre avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor. Você implementa ouvintes de eventos para capturar e responder a eventos (objetos MediaPlayerEvent ).

Seu aplicativo pode recuperar informações de notificação e status. Com essas informações, você também pode criar um sistema de registro para diagnósticos e validação.

## Conteúdo de notificação {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` fornece informações relacionadas ao status do reprodutor.

O TVSDK fornece uma lista cronológica de notificações `MediaPlayerNotification` e cada notificação contém as seguintes informações:

* Um carimbo de data/hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFO, AVISO ou ERRO.
   * `code`: Uma representação numérica da notificação.
   * `name`: Uma descrição legível da notificação, como SEEK_ERROR
   * `metadata`: Pares de chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outro  `MediaPlayerNotification` objeto que afeta diretamente essa notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las a um servidor remoto para registro e representação gráfica.

## Configurar seu sistema de notificação {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Você pode acompanhar as notificações.

O núcleo do sistema de notificação do Player do Primetime é a classe `Notification`, que representa uma notificação independente.

Para receber notificações, ouça as notificações da seguinte maneira:

1. Implemente o retorno de chamada `NotificationEventListener.onNotification()`.
1. O TVSDK transmite um objeto `NotificationEvent` para o retorno de chamada.

   >[!NOTE]
   >
   >Os tipos de notificações são enumerados no enum `Notification.Type`:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Adicionar registro e depuração em tempo real {#section_9D4004308CB243AD9B50818895D10005}

Você pode usar notificações para implementar o logon em tempo real no aplicativo de vídeo.

O sistema de notificação permite coletar informações de registro e depuração para diagnósticos e validação sem estressar o sistema.

>[!IMPORTANT]
>
>O back-end de logon não faz parte de uma configuração de produção e não é esperado que trabalhe com tráfego de alta carga. Se sua implementação não precisar ser absolutamente completa, considere a eficiência da transmissão de dados para evitar sobrecarga do sistema.

Este é um exemplo de como recuperar notificações:

1. Crie um thread de execução com base em temporizador para o aplicativo de vídeo que consulta periodicamente os dados coletados pelo sistema de notificação TVSDK.
1. Se o intervalo do cronômetro for muito grande e o tamanho da lista de eventos for muito pequeno, a lista de eventos de notificação sofrerá sobrefluxo.

   >[!NOTE]
   >
   >Para evitar esse estouro, siga um destes procedimentos:
   >
   >1. Diminua o intervalo de tempo que direciona o thread que pesquisa novos eventos.
   >1. Aumente o tamanho da lista de notificações.


1. Serialize as entradas de evento de notificação mais recentes no formato JSON e envie as entradas para um servidor remoto para pós-processamento.

   >[!NOTE]
   >
   >O servidor remoto pode exibir graficamente os dados fornecidos em tempo real.

1. Para detectar a perda dos eventos de notificação, procure por lacunas na sequência dos valores do índice de eventos.

