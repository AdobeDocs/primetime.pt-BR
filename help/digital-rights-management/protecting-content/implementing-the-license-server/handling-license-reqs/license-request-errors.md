---
title: Tratamento de erros de solicitações de licença
description: Tratamento de erros de solicitações de licença
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Erro de solicitação de licença ao manipular {#license-request-error-handling}

Se ocorrer um erro durante a análise da solicitação, ocorrerá `HandlerParsingException`. Essa exceção inclui informações de erro que são retornadas ao cliente. Se precisar recuperar as informações do erro, chame `HandlerParsingException.getErrorData()`. Se ocorrer um erro durante a geração de uma licença devido aos requisitos da política de DRM que não foram atendidos, ocorrerá um `PolicyEvaluationException`. Essa exceção também inclui `ErrorData` para ser retornado ao cliente.

Consulte a documentação da API para `LicenseRequestMessage.generateLicense()` para obter detalhes sobre como as políticas de DRM são avaliadas durante a geração de licenças.
