---
title: Códigos de erro BEES
description: Códigos de erro BEES
copied-description: true
exl-id: 36c83ee9-7e28-442e-8076-691a1bd43a01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Códigos de erro BEES {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

Se ocorrer um erro durante uma verificação BEES, uma `DRMErrorEvent` serão retornados ao cliente. Você pode analisar as propriedades deste evento para encontrar detalhes sobre a natureza da falha. Um subconjunto de possíveis códigos de erro está listado abaixo.

| Erro | Descrição |
|---|---|
| `3304:305` | Erro de autorização genérico da tentativa do PRIMETIME Cloud DRM de lidar com uma solicitação de autenticação/autorização. Normalmente, não está associada a um problema com o BEES. Se esse erro for encontrado de forma consistente, você deverá enviar um tíquete de problema para a equipe de DRM do Primetime Cloud, juntamente com as informações de diagnóstico. |
| `3329:0` | Erro específico do aplicativo (do Autorizador BEES). Se nenhum código de suberro for retornado, o texto do erro exibirá detalhes do problema. Por exemplo, houve um problema ao analisar a resposta, ou o servidor BEES estava inacessível. |
| `3329:<HTTP error code>` | Uma resposta HTTP diferente de 200 foi emitida pelo servidor BEES. O código de erro HTTP é retornado ao cliente no campo suberror code. Isso pode indicar um problema de configuração ou uma interrupção do servidor BEES. |
| `3329:<x>` | BEES server NÃO PERMITIU a solicitação de licença. O código do suberro e o texto do erro são especificados pelo servidor BEES na resposta JSON `error` e `errorText` propriedades. Esse tipo de resposta não deve ser considerado um erro, mas sim uma resposta de negação regular do seu servidor BEES. |
