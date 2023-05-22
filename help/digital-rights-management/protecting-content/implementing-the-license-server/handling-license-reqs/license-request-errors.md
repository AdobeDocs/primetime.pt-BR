---
title: Tratamento de erros de solicitação de licença
description: Tratamento de erros de solicitação de licença
copied-description: true
exl-id: 7cfdebc5-db2b-4629-98e6-31ad71cb424c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Tratamento de erros de solicitação de licença {#license-request-error-handling}

Se ocorrer um erro durante a análise da solicitação, uma solicitação `HandlerParsingException` ocorre. Essa exceção inclui informações de erro retornadas ao cliente. Se precisar recuperar as informações do erro, é necessário chamar `HandlerParsingException.getErrorData()`. Se ocorrer um erro durante a geração de uma licença devido a requisitos da política de DRM que não foram atendidos, um `PolicyEvaluationException` ocorre. Esta exceção também inclui `ErrorData` para ser devolvido ao cliente.

Consulte a documentação da API para `LicenseRequestMessage.generateLicense()` para obter detalhes sobre como as políticas de DRM são avaliadas durante a geração da licença.
