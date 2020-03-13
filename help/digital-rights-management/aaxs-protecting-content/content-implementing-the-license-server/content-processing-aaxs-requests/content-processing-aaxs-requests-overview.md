---
seo-title: Visão geral
title: Visão geral
uuid: 870c32f5-1119-4fec-abed-25e51dd1ebe3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Visão geral{#overview}

A abordagem geral para lidar com solicitações é criar um manipulador, analisar a solicitação, definir os dados de resposta ou o código de erro e fechar o manipulador.

A classe base usada para lidar com interação de solicitação única/resposta é `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. Uma instância da `HandlerConfiguration` classe é usada para inicializar o manipulador. `HandlerConfiguration` armazena informações de configuração do servidor, incluindo credenciais de transporte, tolerância a carimbo de data e hora, listas de atualização de política e listas de revogação. O manipulador lê os dados da solicitação e analisa-a em uma instância do `RequestMessageBase`. O chamador pode examinar as informações na solicitação e decidir se deve retornar um erro ou uma resposta bem-sucedida (as subclasses de `RequestMessageBase` um método para definir os dados de resposta).

Se a solicitação for bem-sucedida, defina os dados da resposta; caso contrário, invoque `RequestMessageBase.setErrorData()` na falha. Sempre encerre a implementação chamando o `close()` método (recomenda-se que `close()` seja chamado no `finally` bloco de uma `try` instrução). Consulte a documentação de referência da `MessageHandlerBase` API para obter um exemplo de como chamar o manipulador.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>O código de status HTTP 200 (OK) deve ser enviado em resposta a todas as solicitações processadas pelo manipulador. Se o manipulador não puder ser criado devido a um erro de servidor, o servidor poderá responder com outro código de status, como 500 (Internal Server Error).

O cliente usa o URL do License Server especificado no momento da empacotamento como o URL base para todas as solicitações enviadas ao servidor de licenças. Por exemplo, se o URL do servidor for especificado como &quot;<span></span>https://licenseserver.com/path&quot;, o cliente enviará solicitações para &quot;<span></span>https://licenseserver.com/path/flashaccess/...&quot;. Consulte as seções a seguir para obter detalhes sobre o caminho específico usado para cada tipo de solicitação. Ao implementar o servidor de licenças, verifique se ele responde aos caminhos necessários para cada tipo de solicitação.

Uma solicitação de licença pode conter um token de autenticação. Se a autenticação de nome de usuário/senha tiver sido usada, a solicitação poderá conter um `AuthenticationToken` gerado pelo `AuthenticationHandler`SDK, e ele garantirá que o token seja válido antes de emitir uma licença.
