---
seo-title: Processar solicitações de devolução de licença
title: Processar solicitações de devolução de licença
uuid: 994df5af-476a-4ee8-b371-8900241be83d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Processar solicitações de devolução de licença{#handle-license-return-requests}

Se o aplicativo cliente precisar retornar uma licença, ele chamará a `DRMManager.returnVoucher()` API do Actionscript para iniciar o processo. Essa API pode funcionar em um modo `immediateCommit` ou `confirmFirst`. Se `immediateCommit` estiver definido como `true`, o cliente excluirá as licenças locais imediatamente sem aguardar a confirmação do servidor de licenças de que recebeu a solicitação para devolver as licenças. O servidor de licenças DRM da Adobe Primetime deve processar a solicitação e enviar uma resposta ao cliente. Se o servidor de licenças processa ou não a solicitação, como decrementar uma contagem de licenças para um usuário especificado, é decidido pelo servidor de licenças.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

A versão mínima do SDK `Adobe Primetime DRM` necessária é a versão 5; o URL da solicitação é &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Como ocorre com o Cancelamento de registro de domínio, o servidor usa `getRequestPhase()` para determinar se o cliente pode pré-visualização um retorno de licença.
