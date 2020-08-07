---
seo-title: Requisitos para sincronização
title: Requisitos para sincronização
uuid: 19a6ee7e-9580-48bb-a3a6-ff2cedcc796a
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Requisitos para sincronização {#requirements-for-synchronization}

Os requisitos de sincronização especificam a frequência com que o cliente sincroniza seu estado com o servidor. Se o cliente tiver recebido uma licença fora de banda (sem que um servidor de licenças seja contatado), as regras de uso poderão especificar que o cliente deverá enviar mensagens de sincronização ao servidor para sincronizar o horário seguro do cliente e informar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* **Intervalo** de start - especifica o tempo de espera após a última sincronização bem-sucedida para start de outra solicitação de sincronização.
* **Intervalo** de parada rígida - (opcional). Desative a reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* **Forçar probabilidade** de sincronização - (Opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de start.

>[!NOTE]
>
>Esta regra de uso é suportada pelos clientes DRM Primetime versão 3.0 ou posterior. O comportamento de clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças.
