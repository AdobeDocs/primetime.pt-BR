---
title: Códigos de erro BEES
description: Códigos de erro BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Códigos de erro BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Se houver um erro durante uma verificação BEES, um `DRMErrorEvent` será retornado ao cliente. Você pode analisar as propriedades desse evento para encontrar detalhes sobre a natureza da falha. Um subconjunto de possíveis códigos de erro está listado abaixo.

| Erro | Descrição |
|---|---|
| `3304:305` | Erro de Autorização Genérica da DRM do Primetime Cloud que tenta lidar com uma solicitação de autenticação/autorização. Normalmente não está associado a um problema BEES. Se esse erro for encontrado de forma consistente, você deve enviar um tíquete de problemas para a equipe de DRM da Primetime Cloud junto com as informações de diagnóstico. |
| `3329:0` | Erro Específico do Aplicativo (do Autorizador BEES). Se nenhum código de suberro for retornado, o texto do erro exibirá os detalhes do problema. Por exemplo, houve um problema ao analisar a resposta ou o servidor BEES estava inacessível. |
| `3329:<HTTP error code>` | Uma resposta HTTP diferente de 200 foi emitida pelo servidor BEES. O código de erro HTTP é retornado ao cliente no campo do código de suberro. Isso pode indicar um problema de configuração ou uma interrupção do servidor BEES. |
| `3329:<x>` | O servidor BEES DESATIVOU a solicitação de licença. O código de suberro e o texto do erro são especificados pelo servidor BEES nas propriedades `error` e `errorText` da resposta JSON. Esse tipo de resposta não deve ser considerado um erro, mas uma resposta de negação regular do servidor BEES. |