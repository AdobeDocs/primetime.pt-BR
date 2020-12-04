---
seo-title: Tratamento de erros de solicitação de licença
title: Tratamento de erros de solicitação de licença
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Tratamento de erros de solicitação de licença {#license-request-error-handling}

Se ocorrer um erro durante a análise da solicitação, um `HandlerParsingException` ocorrerá. Esta exceção inclui informações de erro que são retornadas ao cliente. Se precisar recuperar as informações do erro, chame `HandlerParsingException.getErrorData()`. Se ocorrer um erro durante a geração de uma licença devido aos requisitos da política de DRM que não foram atendidos, um `PolicyEvaluationException` ocorrerá. Esta exceção também inclui `ErrorData` a ser devolvido ao cliente.

Consulte a documentação da API para `LicenseRequestMessage.generateLicense()` para obter detalhes sobre como as políticas de DRM são avaliadas durante a geração da licença.
