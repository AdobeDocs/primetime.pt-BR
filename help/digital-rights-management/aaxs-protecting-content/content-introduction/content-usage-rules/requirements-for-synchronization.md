---
seo-title: Requisitos para sincronização
title: Requisitos para sincronização
uuid: 976a0ae1-bece-437e-b95b-6cd222525d13
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Requisitos para sincronização{#requirements-for-synchronization}

Especifica a frequência na qual o cliente sincronizará seu estado com o servidor. Se o cliente tiver recebido uma licença fora de banda (sem que um servidor de licenças seja contatado), as regras de uso poderão especificar que o cliente deverá enviar mensagens de sincronização ao servidor para sincronizar o horário seguro do cliente e informar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* Intervalo inicial — Especifica por quanto tempo esperar após a última sincronização bem-sucedida para iniciar outra solicitação de sincronização.
* Intervalo de Parada Rígida — (Opcional). Desative a reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* Forçar Sincronização Probabilidade — (Opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de início.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Essa regra de uso é compatível com os clientes do Adobe Access versão 3.0 e superior. O comportamento de clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças. Consulte, Versão [](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)mínima do cliente.

