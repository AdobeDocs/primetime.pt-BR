---
title: Requisitos para sincronização
description: Requisitos para sincronização
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Requisitos para sincronização {#requirements-for-synchronization}

Requisitos para sincronização especifica a frequência com que o cliente sincroniza seu estado com o servidor. Se o cliente tiver recebido uma licença fora de banda (sem que um servidor de licenças seja contatado), as regras de uso poderão especificar que o cliente deve enviar mensagens de sincronização ao servidor para sincronizar o horário seguro do cliente e relatar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* **Intervalo de Início**  - Especifica o tempo de espera após a última sincronização bem-sucedida para iniciar outra solicitação de sincronização.
* **Intervalo de Parada Rígida**  - (Opcional). Não permitir a reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* **Forçar probabilidade de sincronização**  - (Opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de início.

>[!NOTE]
>
>Essa regra de uso é compatível com os clientes DRM do Primetime versão 3.0 ou posterior. O comportamento em clientes mais antigos depende da versão mínima do cliente compatível com o servidor de licenças.
