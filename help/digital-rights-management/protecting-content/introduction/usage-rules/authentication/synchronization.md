---
title: Requisitos para sincronização
description: Requisitos para sincronização
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Requisitos para sincronização {#requirements-for-synchronization}

Requisitos de sincronização especifica a frequência com que o cliente sincroniza seu estado com o servidor. Se uma licença fora de banda tiver sido emitida ao cliente (sem que um servidor de licenças tenha sido contatado), as regras de uso poderão especificar que o cliente deve enviar mensagens de sincronização ao servidor para sincronizar o horário seguro do cliente e relatar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* **Intervalo de início** - Especifica o tempo de espera após a última sincronização bem-sucedida para iniciar outra solicitação de sincronização.
* **Intervalo de Interrupção Permanente** - (Opcional). Não permitir reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* **Probabilidade de Forçar Sincronização** - (Opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de início.

>[!NOTE]
>
>Esta regra de uso é compatível com clientes DRM do Primetime versão 3.0 ou posterior. O comportamento em clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças.
