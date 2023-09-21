---
title: Lidar com solicitações de devolução de licença
description: Lidar com solicitações de devolução de licença
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Lidar com solicitações de devolução de licença{#handling-license-return-requests}

Se o aplicativo cliente precisar retornar uma licença, ele chamará a API do Actionscript DRMManager.returnVoucher() para iniciar o processo. Essa API pode funcionar em um modo immediateCommit ou em um modo confirmFirst. Se immediateCommit estiver definido como verdadeiro, o cliente excluirá a(s) licença(s) local(is) imediatamente, sem esperar a confirmação do servidor de licenças de que recebeu a solicitação para retornar a(s) licença(s). O servidor de licenças de Acesso ao Adobe deve processar a solicitação e enviar uma resposta ao cliente. Cabe ao servidor de licenças decidir se ele faz ou não algo com a solicitação (como diminuir a contagem de licenças para determinado usuário).

* A classe do manipulador de solicitações é com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* A classe de mensagem de solicitação é com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

A versão mínima do SDK de acesso ao Adobe necessária é a versão 5; o URL da solicitação será &quot; `/flashaccess/lreturn/v5`&quot;. Assim como no caso do cancelamento de registro de domínio, o servidor deve usar `getRequestPhase()` para determinar se o cliente está visualizando uma devolução de licença.
