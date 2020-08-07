---
seo-title: Requisitos para sincronização
title: Requisitos para sincronização
uuid: 976a0ae1-bece-437e-b95b-6cd222525d13
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Requisitos para sincronização{#requirements-for-synchronization}

Especifica a frequência na qual o cliente sincronizará seu estado com o servidor. Se o cliente tiver recebido uma licença fora de banda (sem que um servidor de licenças seja contatado), as regras de uso poderão especificar que o cliente deverá enviar mensagens de sincronização ao servidor para sincronizar o horário seguro do cliente e informar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* Intervalo de start — Especifica por quanto tempo esperar após a última sincronização bem-sucedida para start de outra solicitação de sincronização.
* Intervalo de Parada Rígida — (Opcional). Desative a reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* Forçar Sincronização Probabilidade — (Opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de start.

>[!NOTE]
>
>Esta regra de uso é suportada pelos clientes do Adobe Access versão 3.0 e superior. O comportamento de clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças. Consulte, Versão [](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)mínima do cliente.

