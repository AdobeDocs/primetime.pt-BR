---
description: nulo
seo-description: nulo
seo-title: Regras de negócios de demonstração de modelo de uso
title: Regras de negócios de demonstração de modelo de uso
uuid: c55f85be-5ecb-4a78-b47d-7001ec207d3a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Regras de negócios de demonstração de modelo de uso{#usage-model-demo-business-rules}

Quando um usuário solicita uma licença, o servidor de Implementação de referência verifica os metadados que o cliente enviou para determinar se o conteúdo foi empacotado usando a propriedade `RI_UsageModelDemo`. Se esse for o caso, o servidor aplicará as seguintes regras de negócios.

* Se uma das políticas de DRM exigir autenticação:

   * Se a solicitação contiver um token de autenticação válido, procure o nome do usuário na tabela do banco de dados Cliente.

      Se você não conseguir localizar o nome do usuário, conclua as seguintes tarefas:

      * Se a propriedade `Customer.IsSubscriber` estiver definida como `true`, será necessário gerar uma licença para o modelo de uso *`Subscription`* e enviá-la ao usuário.

      * Procure um registro na tabela do banco de dados `CustomerAuthorization` para saber o nome do usuário e a ID do conteúdo.

      Se você puder localizar o registro do usuário, conclua as seguintes tarefas:

      * Se a propriedade `CustomerAuthorization.UsageType` estiver definida como `DTO`, gere uma licença para o modelo de utilização DTO e envie-a para o utilizador.

      * Se a propriedade `CustomerAuthorization.UsageType` estiver definida como `VOD`, gere uma licença para o modelo de uso de VOD e envie-a ao usuário.

      Se nenhuma das políticas de DRM permitir acesso anônimo, conclua as seguintes tarefas:

      * Se não houver um token de autenticação válido na solicitação, será necessário retornar um erro de &quot;autenticação obrigatória&quot;.
      * Caso contrário, retorne um erro &quot;não autorizado&quot;.



* Se uma das políticas de DRM permitir acesso anônimo, gere uma licença para o modelo de uso financiado pelo anúncio e envie-a ao usuário.

