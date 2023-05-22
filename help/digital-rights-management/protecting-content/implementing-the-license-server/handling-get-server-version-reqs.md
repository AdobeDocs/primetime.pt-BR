---
title: Lidar com solicitações de Obtenção de Versão do Servidor
description: Lidar com solicitações de Obtenção de Versão do Servidor
copied-description: true
exl-id: 86a1bbe3-2ae4-4d4e-be51-fbbeb32147c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
