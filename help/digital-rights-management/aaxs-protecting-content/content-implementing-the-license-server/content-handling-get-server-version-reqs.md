---
title: Lidando com solicitações de versão do Get Server
description: Lidando com solicitações de versão do Get Server
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Lidando com solicitações de versão do servidor Get{#handling-get-server-version-requests}

O cliente Adobe Access 3.0 e superior envia uma solicitação Get Server Version para determinar os recursos do servidor. Todos os servidores que usam o Adobe Access SDK 3.0 e superior devem implementar suporte para solicitações Get Server Version.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* O URL da solicitação deve ser &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Para o SDK 4.0 e superior do Adobe Access, a resposta a uma solicitação Get Server Version indica aos clientes que o servidor suporta as versões 3 e 4 do protocolo Adobe Access.
