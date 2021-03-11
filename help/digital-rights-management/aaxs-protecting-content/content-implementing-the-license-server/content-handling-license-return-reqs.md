---
title: Tratamento de solicitações de retorno de licença
description: Tratamento de solicitações de retorno de licença
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Lidando com solicitações de retorno de licença{#handling-license-return-requests}

Se o aplicativo cliente precisar retornar uma licença, ele chamará a API do Actionscript DRMManager.returnVoucher() para iniciar o processo. Essa API pode funcionar em um modo immediateCommit ou em um modo confirmFirst. Se immediateCommit for definido como true, o cliente excluirá as licenças locais imediatamente, sem esperar a confirmação do servidor de licenças de que recebeu a solicitação para retornar as licenças. O servidor de licenças de Adobe Access deve processar a solicitação e enviar uma resposta ao cliente. Se o servidor de licenças realmente faz alguma coisa com a solicitação (como decrementar uma contagem de licenças para o usuário em questão) cabe ao servidor de licenças decidir.

* A classe do manipulador de solicitações é com.adobe.flashaccess.sdk.protocol.licencisereturn.LicenseReturnHandler
* A classe de mensagem de solicitação é com.adobe.flashaccess.sdk.protocol.licenseReturn.LicenseReturnRequestMessage

A versão mínima necessária do SDK de Acesso ao Adobe é a versão 5; o URL da solicitação será &quot; `/flashaccess/lreturn/v5`&quot;. Assim como com o Cancelamento de registro de domínio, o servidor deve usar `getRequestPhase()` para determinar se o cliente está visualizando um retorno de licença.
