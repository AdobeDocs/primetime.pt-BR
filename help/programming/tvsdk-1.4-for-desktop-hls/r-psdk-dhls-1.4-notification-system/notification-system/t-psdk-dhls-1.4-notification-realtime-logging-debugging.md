---
description: Você pode usar as notificações para implementar o registro em tempo real no aplicativo de vídeo.
title: Adicionar depuração e registro em tempo real
exl-id: 06ba7207-bb6e-4f77-8575-746505b131bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Adicionar depuração e registro em tempo real{#add-real-time-logging-and-debugging}

Você pode usar as notificações para implementar o registro em tempo real no aplicativo de vídeo.

O sistema de notificação permite coletar informações de registro e depuração para diagnóstico e validação sem sobrecarregar o sistema.

>[!IMPORTANT]
>
>O back-end de registro não faz parte de uma configuração de produção e não é esperado que manipule o tráfego de carga alta. Se a implementação não precisar estar totalmente completa, considere a eficiência da transmissão de dados para evitar sobrecarga do sistema.

Este é um exemplo de como recuperar notificações.

1. Crie um thread de execução baseado em cronômetro para seu aplicativo de vídeo que consulte periodicamente os dados coletados pelo sistema de notificação TVSDK.

1. Se o intervalo do cronômetro for muito grande e o tamanho da lista de eventos for muito pequeno, a lista de eventos de notificação estourará. Para evitar esse excesso, siga um destes procedimentos:

   * Diminuir o intervalo de tempo que orienta o thread que pesquisa novos eventos.
   * Aumente o tamanho da lista de notificações.

1. Serialize as entradas de evento de notificação mais recentes no formato JSON e envie as entradas para um servidor remoto para pós-processamento.

   O servidor remoto poderia exibir graficamente os dados fornecidos em tempo real.
1. Para detectar a perda de eventos de notificação, procure por lacunas na sequência de valores de índice de evento.

   Cada evento de notificação tem um valor de índice que é incrementado automaticamente pelo `NotificationHistory` classe.
