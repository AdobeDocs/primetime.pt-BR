---
description: Você pode usar notificações para implementar o logon em tempo real no aplicativo de vídeo.
seo-description: Você pode usar notificações para implementar o logon em tempo real no aplicativo de vídeo.
seo-title: Adicionar registro e depuração em tempo real
title: Adicionar registro e depuração em tempo real
uuid: 037daf57-a1b3-4b42-ac51-81179fb36915
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Adicionar registro e depuração em tempo real{#add-real-time-logging-and-debugging}

Você pode usar notificações para implementar o logon em tempo real no aplicativo de vídeo.

O sistema de notificação permite coletar informações de registro e depuração para diagnóstico e validação sem estressar excessivamente o sistema.

>[!IMPORTANT]
>
>O back-end de logon não faz parte de uma configuração de produção e não é esperado que trate de tráfego de alta carga. Se sua implementação não precisar ser totalmente concluída, considere a eficiência da transmissão de dados para evitar sobrecarregar seu sistema.

Este é um exemplo de como recuperar notificações.

1. Crie um thread de execução com base em temporizador para seu aplicativo de vídeo que query periodicamente os dados coletados pelo sistema de notificação TVSDK.

1. Se o intervalo do temporizador for muito grande e o tamanho da lista do evento for muito pequeno, a lista do evento de notificação estourará. Para evitar esse sobrefluxo, execute um dos procedimentos a seguir:

   * Diminua o intervalo de tempo que direciona o thread que pesquisa novos eventos.
   * Aumente o tamanho da lista de notificação.

1. Serialize as entradas mais recentes do evento de notificação no formato JSON e envie as entradas para um servidor remoto para pós-processamento.

   O servidor remoto poderia então exibir graficamente os dados fornecidos em tempo real.
1. Para detectar a perda de eventos de notificação, procure por lacunas na sequência de valores de índice de evento.

   Cada evento de notificação tem um valor de índice que é incrementado automaticamente pela classe `session.NotificationHistory`.
