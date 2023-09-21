---
title: Lidar com solicitações de Obtenção de Versão do Servidor
description: Lidar com solicitações de Obtenção de Versão do Servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Lidar com solicitações de Obtenção de Versão do Servidor{#handling-get-server-version-requests}

O Adobe Access client 3.0 e superior envia uma solicitação Get Server Version para determinar as capacidades do servidor. Todos os servidores que usam o Adobe Access SDK 3.0 e superior devem implementar o suporte para solicitações Get Server Version.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* O URL da solicitação deve ser &quot;URL do Servidor de Licença nos metadados&quot; + &quot;/flashaccess/getServerVersion/v3&quot;

Para o Adobe Access SDK 4.0 e superior, a resposta a uma solicitação Obter versão do servidor indica aos clientes que o servidor suporta as versões 3 e 4 do protocolo Adobe Access.
