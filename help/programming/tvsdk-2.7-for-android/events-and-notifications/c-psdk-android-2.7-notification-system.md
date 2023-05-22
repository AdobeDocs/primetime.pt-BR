---
description: Os objetos MediaPlayerStatus fornecem informações sobre as alterações no status do player. Os objetos de notificação fornecem informações sobre avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor. Você implementa ouvintes de eventos para capturar e responder a eventos (objetos MediaPlayerEvent).
title: Notificações e eventos para status, atividade, erros e registro do player
exl-id: c25e834e-ffa0-444c-9285-331e6841ac29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Notificações e eventos para status, atividade, erros e registro do player {#notifications-and-events-for-player-status-activity-errors-and-logging}

Eventos e notificações ajudam você a gerenciar os aspectos assíncronos do aplicativo de vídeo.

Os objetos MediaPlayerStatus fornecem informações sobre as alterações no status do player. Os objetos de notificação fornecem informações sobre avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor. Você implementa ouvintes de eventos para capturar e responder a eventos (objetos MediaPlayerEvent).

Seu aplicativo pode recuperar informações de notificação e status. Usando essas informações, você também pode criar um sistema de registro para diagnóstico e validação.

## Conteúdo da notificação {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` O fornece informações relacionadas ao status do reprodutor.

O TVSDK fornece uma lista cronológica de `MediaPlayerNotification` e cada notificação contém as seguintes informações:

* Um carimbo de data e hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFORMAÇÕES, AVISO ou ERRO.
   * `code`: uma representação numérica da notificação.
   * `name`: uma descrição legível da notificação, como SEEK_ERROR
   * `metadata`: Pares de chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` O fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outra `MediaPlayerNotification` objeto que afeta diretamente esta notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las a um servidor remoto para registro e representação gráfica.

## Configurar seu sistema de notificação {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Você pode acompanhar as notificações.

O núcleo do sistema de notificação do Primetime Player é o `Notification` classe, que representa uma notificação independente.

Para receber notificações, acompanhe as notificações da seguinte maneira:

1. Implementar o `NotificationEventListener.onNotification()` retorno de chamada.
1. O TVSDK passa um `NotificationEvent` para o retorno de chamada.

   >[!NOTE]
   >
   >Os tipos de notificações são enumerados no `Notification.Type` enum:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Adicionar depuração e registro em tempo real {#section_9D4004308CB243AD9B50818895D10005}

Você pode usar as notificações para implementar o registro em tempo real no aplicativo de vídeo.

O sistema de notificação permite coletar informações de registro e depuração para diagnóstico e validação sem estressar o sistema.

>[!IMPORTANT]
>
>O back-end de registro não faz parte de uma configuração de produção e não é esperado que manipule o tráfego de carga alta. Se a implementação não precisar estar totalmente completa, considere a eficiência da transmissão de dados para evitar sobrecarga do sistema.

Este é um exemplo de como recuperar notificações:

1. Crie um thread de execução baseado em cronômetro para seu aplicativo de vídeo que consulte periodicamente os dados coletados pelo sistema de notificação TVSDK.
1. Se o intervalo do cronômetro for muito grande e o tamanho da lista de eventos for muito pequeno, a lista de eventos de notificação estourará.

   >[!NOTE]
   >
   >Para evitar esse excesso, siga um destes procedimentos:
   >
   >1. Diminuir o intervalo de tempo que orienta o thread que pesquisa novos eventos.
   >1. Aumente o tamanho da lista de notificações.


1. Serialize as entradas de evento de notificação mais recentes no formato JSON e envie as entradas para um servidor remoto para pós-processamento.

   >[!NOTE]
   >
   >O servidor remoto pode exibir graficamente os dados fornecidos em tempo real.

1. Para detectar a perda de eventos de notificação, procure por lacunas na sequência de valores de índice de evento.
