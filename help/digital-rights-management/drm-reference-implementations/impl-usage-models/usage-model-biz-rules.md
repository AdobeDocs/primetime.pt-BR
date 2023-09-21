---
title: Regras de negócios da demonstração do modelo de uso
description: Regras de negócios da demonstração do modelo de uso
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Regras de negócios da demonstração do modelo de uso{#usage-model-demo-business-rules}

Quando um usuário solicita uma licença, o servidor de implementação de referência verifica os metadados enviados pelo cliente para determinar se o conteúdo foi empacotado usando o `RI_UsageModelDemo` propriedade. Se esse for o caso, o servidor aplicará as seguintes regras de negócios.

* Se uma das políticas DRM exigir autenticação:

   * Se a solicitação tiver um token de autenticação válido, procure o nome do usuário na tabela de banco de dados Cliente.

     Se não conseguir localizar o nome do usuário, conclua as seguintes tarefas:

      * Se a variável `Customer.IsSubscriber` propriedade está definida como `true`, é necessário gerar uma licença para o *`Subscription`* modelo de uso e envie-o para o usuário.

      * Pesquisar um registro no `CustomerAuthorization` tabela de banco de dados para o nome do usuário e a ID de conteúdo.

     Se você puder localizar o registro do usuário, conclua as seguintes tarefas:

      * Se a variável `CustomerAuthorization.UsageType` propriedade está definida como `DTO`, gere uma licença para o modelo de uso DTO e envie-a para o usuário.

      * Se a variável `CustomerAuthorization.UsageType` propriedade está definida como `VOD`, gere uma licença para o modelo de uso de VOD e envie-a ao usuário.

     Se nenhuma das políticas DRM permitir acesso anônimo, conclua as seguintes tarefas:

      * Se não houver um token de autenticação válido na solicitação, você precisará retornar um erro &quot;autenticação necessária&quot;.
      * Caso contrário, retorne um erro &quot;não autorizado&quot;.

* Se uma das políticas DRM permitir acesso anônimo, gere uma licença para o modelo de uso financiado por anúncio e envie-a para o usuário.
