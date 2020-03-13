---
seo-title: Tratamento de solicitações de devolução de licença
title: Tratamento de solicitações de devolução de licença
uuid: d184faea-88cb-44f3-a253-e5314d577f17
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Tratamento de solicitações de devolução de licença{#handling-license-return-requests}

Se o aplicativo cliente precisar retornar uma licença, ele chamará a API do Actionscript DRMManager.returnVoucher() para iniciar o processo. Essa API pode funcionar em um modo imediatoCommit ou um modo confirmFirst. Se o imediatoCommit estiver definido como true, o cliente excluirá as licenças locais imediatamente, sem aguardar a confirmação do servidor de licenças de que recebeu a solicitação para retornar as licenças. O servidor de licenças do Adobe Access deve processar a solicitação e enviar uma resposta ao cliente. Se o servidor de licenças realmente faz ou não alguma coisa com a solicitação (como decrementar uma contagem de licenças para o usuário em questão) é uma decisão do servidor de licenças.

* A classe do manipulador de solicitações é com.adobe.flashaccess.sdk.protocol.licenseReturn.LicenseReturnHandler
* A classe de mensagem de solicitação é com.adobe.flashaccess.sdk.protocol.licenseReturn.LicenseReturnRequestMessage

A versão mínima do SDK do Adobe Access exigida é a versão 5; o URL da solicitação será &quot; `/flashaccess/lreturn/v5`&quot;. Como ocorre com o Cancelamento de registro de domínio, o servidor deve usar `getRequestPhase()` para determinar se o cliente está visualizando uma devolução de licença.
