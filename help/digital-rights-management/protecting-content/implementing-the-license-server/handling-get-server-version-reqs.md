---
title: Gerenciar solicitações de versão do servidor Get
description: Gerenciar solicitações de versão do servidor Get
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Gerenciar solicitações de Obter versão do servidor {#handle-get-server-version-requests}

O cliente Adobe Primetime DRM 3.0 ou posterior envia uma solicitação Get Server Version para determinar os recursos do servidor. Todos os servidores que usam Primetime DRM SDK 3.0 ou posterior devem implementar o suporte para solicitações Get Server Version.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* O URL da solicitação deve ser &quot;URL do License Server em metadados&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Para o Primetime DRM SDK 4.0 ou posterior, a resposta a uma solicitação Get Server Version indica aos clientes que o servidor suporta as versões 3 e 4 do protocolo Primetime DRM.
