---
title: Lidar com solicitações de Obtenção de Versão do Servidor
description: Lidar com solicitações de Obtenção de Versão do Servidor
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Lidar com solicitações de Obtenção de Versão do Servidor {#handle-get-server-version-requests}

O cliente Adobe Primetime DRM 3.0 ou posterior envia uma solicitação Obter Versão do Servidor para determinar os recursos do servidor. Todos os servidores que usam o Primetime DRM SDK 3.0 ou posterior devem implementar o suporte para solicitações Obter Versão do Servidor.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* O URL da solicitação deve ser &quot;URL do servidor de licenças nos metadados&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Para o Primetime DRM SDK 4.0 ou posterior, a resposta a uma solicitação Obter versão do servidor indica aos clientes que o servidor oferece suporte às versões 3 e 4 do protocolo DRM Primetime.
