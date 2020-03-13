---
seo-title: Processar solicitações de Obter versão do servidor
title: Processar solicitações de Obter versão do servidor
uuid: 6e287f58-2ad2-428a-a76a-6847d06b0fd8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Processar solicitações de Obter versão do servidor {#handle-get-server-version-requests}

O cliente Adobe Primetime DRM 3.0 ou posterior envia uma solicitação Get Server Version para determinar os recursos do servidor. Todos os servidores que usam o Primetime DRM SDK 3.0 ou posterior devem implementar suporte para solicitações Get Server Version.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.getversion.GetServerVersionRequestMessage`
* O URL da solicitação deve ser &quot;URL do License Server em metadados&quot; + &quot; [!DNL /flashaccess/getServerVersion/v3]&quot;

Para o Primetime DRM SDK 4.0 ou posterior, a resposta a uma solicitação Get Server Version indica aos clientes que o servidor suporta as versões 3 e 4 do protocolo Primetime DRM.
