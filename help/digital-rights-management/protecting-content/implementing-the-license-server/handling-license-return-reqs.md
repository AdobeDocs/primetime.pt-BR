---
title: Lidar com solicitações de devolução de licença
description: Lidar com solicitações de devolução de licença
copied-description: true
exl-id: de577cb9-4ede-440e-8b71-1b39c6cc3c5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Lidar com solicitações de devolução de licença{#handle-license-return-requests}

Se o aplicativo cliente precisar retornar uma licença, ele chamará a `DRMManager.returnVoucher()` API do Actionscript para iniciar o processo. Essa API pode funcionar em um `immediateCommit` ou um `confirmFirst` modo. Se `immediateCommit` está definida como `true`, o cliente então exclui a(s) licença(s) local(is) imediatamente sem esperar pela confirmação do servidor de licenças de que recebeu a solicitação para retornar a(s) licença(s). O servidor de licenças DRM da Adobe Primetime deve processar a solicitação e enviar uma resposta ao cliente. Se o servidor de licenças processa ou não a solicitação, como diminuir uma contagem de licenças para um usuário especificado, isso é decidido pelo servidor de licenças.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

O mínimo `Adobe Primetime DRM` A versão do SDK necessária é a 5; o URL da solicitação é &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Assim como ocorre com o cancelamento de registro de domínio, o servidor usa `getRequestPhase()` para determinar se o cliente pode visualizar uma devolução de licença.
