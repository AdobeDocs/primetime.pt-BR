---
title: Requisitos para sincronização
description: Requisitos para sincronização
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Requisitos para sincronização{#requirements-for-synchronization}

Especifica a frequência com que o cliente sincronizará seu estado com o servidor. Se uma licença fora de banda tiver sido emitida ao cliente (sem que um servidor de licenças tenha sido contatado), as regras de uso poderão especificar que o cliente deve enviar mensagens de sincronização ao servidor para sincronizar o tempo seguro do cliente e relatar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* Intervalo de Início — Especifica o tempo de espera após a última sincronização bem-sucedida para iniciar outra solicitação de sincronização.
* Intervalo de Interrupção Permanente — (Opcional). Não permitir reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* Probabilidade de sincronização forçada — (opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de início.

>[!NOTE]
>
>Esta regra de uso é suportada pelos clientes Adobe Access versões 3.0 e superiores. O comportamento em clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças. Consulte [Versão Mínima do Cliente](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

