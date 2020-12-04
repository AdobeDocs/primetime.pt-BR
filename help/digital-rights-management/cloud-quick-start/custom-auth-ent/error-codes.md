---
seo-title: Códigos de erro BEES
title: Códigos de erro BEES
uuid: 7b2d0dd1-9a43-47e3-b932-a4eaf784ae7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Códigos de erro BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Se houver um erro durante uma verificação BEES, um `DRMErrorEvent` será retornado ao cliente. Você pode analisar essas propriedades do evento para encontrar detalhes sobre a natureza da falha. Um subconjunto de possíveis códigos de erro está listado abaixo.

| Erro | Descrição |
|---|---|
| `3304:305` | Erro de autorização genérico do DRM da Primetime Cloud tentando lidar com uma solicitação de autenticação/autorização. Geralmente não está associado a um problema de BEES. Se esse erro for consistentemente encontrado, você deve enviar um ticket de problema para a equipe de DRM da Primetime Cloud junto com as informações de diagnóstico. |
| `3329:0` | Erro específico do aplicativo (do Autor do BEES). Se nenhum código de suberro for retornado, o texto do erro exibirá detalhes do problema. Por exemplo, houve um problema ao analisar a resposta, ou o servidor BEES foi inacessível. |
| `3329:<HTTP error code>` | Uma resposta HTTP diferente de 200 foi emitida pelo servidor BEES. O código de erro HTTP é retornado ao cliente no campo do código de suberro. Isso pode indicar um problema de configuração ou uma interrupção do servidor BEES. |
| `3329:<x>` | O servidor BEES DESATIVOU a solicitação de licença. O código de suberro e o texto do erro são especificados pelo servidor BEES dentro das propriedades `error` e `errorText` da resposta JSON. Esse tipo de resposta não deve ser considerado um erro, mas sim uma resposta de negação regular do servidor BEES. |