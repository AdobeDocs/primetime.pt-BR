---
title: Processar solicitações de Retorno de Licença
description: Processar solicitações de Retorno de Licença
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Gerenciar solicitações de retorno de licença{#handle-license-return-requests}

Se o aplicativo cliente precisar retornar uma licença, ele chamará a API do ActionScript `DRMManager.returnVoucher()` para iniciar o processo. Essa API pode funcionar em um modo `immediateCommit` ou `confirmFirst`. Se `immediateCommit` estiver definido como `true`, o cliente excluirá a(s) licença(s) local(ais) imediatamente sem esperar a confirmação do servidor de licença de que recebeu a solicitação para retornar a(s) licença(s). O servidor de licenças do DRM da Adobe Primetime deve processar a solicitação e enviar uma resposta ao cliente. Se o servidor de licenças processa ou não a solicitação, como decrementar uma contagem de licenças para um usuário especificado, é decidido pelo servidor de licenças.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

A versão mínima `Adobe Primetime DRM` do SDK necessária é a versão 5; o URL da solicitação é &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Assim como com o Cancelamento de registro de domínio, o servidor usa `getRequestPhase()` para determinar se o cliente pode visualizar um retorno de licença.
