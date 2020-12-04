---
seo-title: Tratamento de solicitações de Obter versão do servidor
title: Tratamento de solicitações de Obter versão do servidor
uuid: a3084faa-cf3d-45cc-a244-298308c4cf15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Tratamento de solicitações Get Server Version{#handling-get-server-version-requests}

O cliente Adobe Access 3.0 e superior envia uma solicitação Get Server Version para determinar os recursos do servidor. Todos os servidores que usam o SDK 3.0 e superior do Adobe Access devem implementar suporte para solicitações Get Server Version.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* O URL da solicitação deve ser &quot;URL do License Server em metadados&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Para o SDK 4.0 e superior do Adobe Access, a resposta a uma solicitação Get Server Version indica aos clientes que o servidor suporta as versões 3 e 4 do protocolo Adobe Access.
