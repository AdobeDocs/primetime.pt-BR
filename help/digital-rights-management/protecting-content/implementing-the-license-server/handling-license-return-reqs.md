---
seo-title: Processar solicitações de devolução de licença
title: Processar solicitações de devolução de licença
uuid: 994df5af-476a-4ee8-b371-8900241be83d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Processar solicitações de devolução de licença{#handle-license-return-requests}

Se o aplicativo cliente precisar retornar uma licença, ele chamará a API do `DRMManager.returnVoucher()` Actionscript para iniciar o processo. Essa API pode funcionar em um `immediateCommit` modo ou em um `confirmFirst` modo. Se `immediateCommit` estiver definido como `true`, o cliente excluirá as licenças locais imediatamente, sem aguardar a confirmação do servidor de licenças de que recebeu a solicitação para retornar as licenças. O servidor de licenças DRM do Adobe Primetime deve processar a solicitação e enviar uma resposta ao cliente. Se o servidor de licenças processa ou não a solicitação, como decrementar uma contagem de licenças para um usuário especificado, é decidido pelo servidor de licenças.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

A versão mínima `Adobe Primetime DRM` do SDK necessária é a versão 5; o URL da solicitação é &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Como ocorre com o Cancelamento de registro de domínio, o servidor usa `getRequestPhase()` para determinar se o cliente pode visualizar um retorno de licença.
