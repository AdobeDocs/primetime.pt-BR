---
title: Regras de negócios de demonstração do modelo de uso
description: Regras de negócios de demonstração do modelo de uso
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Regras de negócios de demonstração do modelo de uso{#usage-model-demo-business-rules}

Quando um usuário solicita uma licença, o servidor de Implementação de Referência verifica os metadados que o cliente enviou, para determinar se o conteúdo foi empacotado usando a propriedade `RI_UsageModelDemo`. Se esse for o caso, o servidor aplicará as seguintes regras de negócios.

* Se uma das políticas de DRM exigir autenticação:

   * Se a solicitação contiver um token de autenticação válido, procure o nome do usuário na tabela do banco de dados do Cliente.

      Se não for possível localizar o nome do usuário, conclua as seguintes tarefas:

      * Se a propriedade `Customer.IsSubscriber` estiver definida como `true`, será necessário gerar uma licença para o modelo de uso *`Subscription`* e enviá-la ao usuário.

      * Procure por um registro na tabela do banco de dados `CustomerAuthorization` para o nome do usuário e a ID do conteúdo.

      Se você puder localizar o registro do usuário, conclua as seguintes tarefas:

      * Se a propriedade `CustomerAuthorization.UsageType` estiver definida como `DTO`, gere uma licença para o modelo de uso DTO e envie-a para o usuário.

      * Se a propriedade `CustomerAuthorization.UsageType` estiver definida como `VOD`, gere uma licença para o modelo de uso de VOD e envie-a para o usuário.

      Se nenhuma das políticas de DRM permitir acesso anônimo, conclua as seguintes tarefas:

      * Se não houver um token de autenticação válido na solicitação, será necessário retornar um erro de &quot;autenticação necessária&quot;.
      * Caso contrário, retorne um erro &quot;não autorizado&quot;.



* Se uma das políticas de DRM permitir o acesso anônimo, gere uma licença para o modelo de uso financiado pelo anúncio e envie-a para o usuário.

