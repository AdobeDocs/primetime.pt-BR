---
description: Você pode usar notificações para implementar o logon em tempo real no aplicativo de vídeo.
title: Adicionar registro e depuração em tempo real
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Adicionar registro e depuração em tempo real{#add-real-time-logging-and-debugging}

Você pode usar notificações para implementar o logon em tempo real no aplicativo de vídeo.

O sistema de notificação permite coletar informações de registro e depuração para diagnósticos e validação sem sobrecarregar o sistema.

>[!IMPORTANT]
>
>O back-end de logon não faz parte de uma configuração de produção e não é esperado que trabalhe com tráfego de alta carga. Se sua implementação não precisar ser absolutamente completa, considere a eficiência da transmissão de dados para evitar sobrecarga do sistema.

Este é um exemplo de como recuperar notificações.

1. Crie um thread de execução com base em temporizador para o aplicativo de vídeo que consulta periodicamente os dados coletados pelo sistema de notificação TVSDK.

1. Se o intervalo do cronômetro for muito grande e o tamanho da lista de eventos for muito pequeno, a lista de eventos de notificação sofrerá sobrefluxo. Para evitar esse estouro, siga um destes procedimentos:

   * Diminua o intervalo de tempo que direciona o thread que pesquisa novos eventos.
   * Aumente o tamanho da lista de notificações.

1. Serialize as entradas de evento de notificação mais recentes no formato JSON e envie as entradas para um servidor remoto para pós-processamento.

   O servidor remoto poderia então exibir graficamente os dados fornecidos em tempo real.
1. Para detectar a perda dos eventos de notificação, procure por lacunas na sequência dos valores do índice de eventos.

   Cada evento de notificação tem um valor de índice que é incrementado automaticamente pela classe `session.NotificationHistory`.
