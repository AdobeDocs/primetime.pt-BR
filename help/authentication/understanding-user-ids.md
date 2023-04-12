---
title: Como entender IDs de usuário
description: Como entender IDs de usuário
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Como entender IDs de usuário {#understanding-user-ids}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

Conceitualmente, cada usuário que inicia um fluxo de direito é associado a uma única ID de usuário exclusiva. No entanto, durante um fluxo de direito, essa ID de usuário pode ser apresentada de diferentes maneiras, dependendo da API da qual você obtém a ID.

O `sessionGUID` no Token de mídia curta é a forma segura da ID do usuário, que está disponível por meio do `sendTrackingData()` chame. Em todas as integrações atuais, esse é um GUID persistente para o usuário ao longo do tempo e dos dispositivos. A origem do GUID começa com a ID de usuário da resposta de autenticação proveniente do MVPD. No entanto, alguns MVPDs podem mudar de ideia no futuro e começar a enviar um GUID transitório. Se um Programador quiser garantir que a ID de usuário de origem do MVPD na resposta do AuthN seja persistente, ele deverá providenciar isso em seus contratos com MVPDs.

Estas são as diferentes maneiras em que a ID de usuário é representada nas APIs de autenticação do Adobe Primetime:

| Propriedade | Finalidade | Hash | Assinado digitalmente | Descrição |
| --- | --- | --- | --- | --- |
| propriedade GUID sendTrackingData() | Rastreamento/análise | Sim | Não | - A ID de usuário do MVPD, com hash por Adobe. A ID de usuário não pode ser rastreada de volta para a origem do MVPD. </br> </br> - Este formulário da ID não é assinado digitalmente, por isso não é seguro para prevenção de fraudes. No entanto, é bom o suficiente para o analytics.  </br> </br> - Esse formulário da ID de usuário é fornecido no lado do cliente em todos os eventos gerados pela autenticação da Adobe Primetime no fluxo AuthN/AuthZ. |
| Propriedade sessionGUID do token de mídia curto | Rastreamento de fraude de uso simultâneo | Sim | Sim | - Essa é a mesma ID de usuário por sendTrackingData(). No entanto, essa é assinada digitalmente para proteger sua integridade e é boa o suficiente para ser usada no rastreamento de fraude. </br> </br> - Ele deve ser processado no lado do servidor após o uso da biblioteca do validador e pode ser analisado em busca de padrões de fraude antes de liberar o fluxo de vídeo para o cliente.  Fazer qualquer uma dessas tarefas depende do Programador. |
| propriedade userMetadata() userID | Vinculação de contas, investigação de fraude com MVPD | Não | Não | - Essa propriedade permite que o Adobe exponha a ID de usuário MVPD de origem real ao Programador. </br> </br> - Na configuração do Adobe, ele pode ser definido como criptografado ou não (dependendo da preferência MVPD). Se estiver criptografado, ele será criptografado com a chave pública pelo certificado do Programador fornecido ao Adobe, para que não seja exposto de forma clara ao cliente. </br> </br> - Isso fornece ao programador o ID de usuário real do MVPD, então é algo que pode ser usado para vinculação de contas ou investigação de fraude diretamente com o MVPD. |


**Em conclusão**

* Em geral, o MVPD fornece uma ID exclusiva persistente <u>e o transmite para o Adobe na autenticação bem-sucedida</u>. Geralmente é consistente em todas as redes. A exceção é o MVPD Comcast, que fornece uma ID de usuário diferente para cada canal.

* A ID de usuário do MVPD não contém PII e NÃO é um número de conta. Ele não precisa ser exposto em um formulário criptografado, pois validamos com todos os MVPDs que nenhum PII está sendo enviado.

A forma como você usa a ID de usuário depende do caso de uso:

* Se for necessário para rastreamento/análise, o local mais prático é obtê-la de `sendTrackingData()`.
* Se for necessário no lado do servidor para liberação de fluxo, fraude ou dados operacionais, é possível obtê-los do validador de Token de mídia.
* Se precisar disso para vinculação de contas e fraude mais profunda, verifique sua disponibilidade com o Adobe contact.

