---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Visão geral{#overview}

A abordagem geral para lidar com solicitações é criar um manipulador, analisar a solicitação, definir os dados de resposta ou o código de erro e fechar o manipulador.

A classe base usada para lidar com interação de solicitação/resposta única é `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Uma instância da classe `HandlerConfiguration` é usada para inicializar o manipulador. `HandlerConfiguration` armazena informações de configuração do servidor, incluindo credenciais de transporte, tolerância ao carimbo de data e hora, listas de atualização de política e listas de revogação. O manipulador lê os dados da solicitação e analisa a solicitação em uma instância de  `RequestMessageBase`. O chamador pode examinar as informações na solicitação e decidir se retorna um erro ou uma resposta bem-sucedida (as subclasses de `RequestMessageBase` fornecem um método para definir os dados de resposta).

Se a solicitação for bem-sucedida, defina os dados de resposta; caso contrário, chame `RequestMessageBase.setErrorData()` sobre falha. Encerre sempre a implementação chamando o método `close()` (recomenda-se que `close()` seja chamado no bloco `finally` de uma instrução `try`). Consulte a documentação de referência da API `MessageHandlerBase` para obter um exemplo de como chamar o manipulador.

>[!NOTE]
>
>O código de status HTTP 200 (OK) deve ser enviado em resposta a todas as solicitações processadas pelo manipulador. Se o manipulador não puder ser criado devido a um erro de servidor, o servidor poderá responder com outro código de status, como 500 (Internal Server Error).

O cliente usa o URL do License Server especificado no momento do empacotamento como o URL base para todas as solicitações enviadas para o servidor de licenças. Por exemplo, se o URL do servidor for especificado como &quot;ht<span></span>tps://licenseserver.com/path&quot;, o cliente enviará solicitações para &quot;ht<span></span>tps://licenseserver.com/path/flashaccess/...&quot;. Consulte as seções a seguir para obter detalhes sobre o caminho específico usado para cada tipo de solicitação. Ao implementar o servidor de licenças, verifique se ele responde aos caminhos necessários para cada tipo de solicitação.

Uma solicitação de licença pode conter um token de autenticação. Se a autenticação de nome de usuário/senha tiver sido usada, a solicitação poderá conter um `AuthenticationToken` gerado pelo `AuthenticationHandler`, e o SDK garantirá que o token seja válido antes de emitir uma licença.
