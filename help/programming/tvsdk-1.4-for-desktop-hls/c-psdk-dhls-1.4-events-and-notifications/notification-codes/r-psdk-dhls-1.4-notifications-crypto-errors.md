---
description: O módulo de criptografia do mecanismo de vídeo Adobe retorna essas notificações no objeto de metadados NATIVE_ERROR.
title: Valores de criptografia NATIVE_ERROR
exl-id: c14b35c1-ed91-4a44-b826-fd6a05dbe345
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 8%

---

# NATIVE_ERROR: valores de criptografia{#native-error-crypto-values}

O módulo de criptografia do mecanismo de vídeo Adobe retorna essas notificações no objeto de metadados NATIVE_ERROR.

| Valor para a chave de metadados RUNTIME_CODE | Valor para a chave de metadados RUNTIME_CODE_MESSAGE | Significado |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | Não há suporte para o algoritmo que está sendo usado. |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | Os dados estão corrompidos. |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | Buffer muito pequeno. |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | Certificado inválido. |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | Atualização do resumo. |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | Término do resumo. |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | Parâmetro inválido. |
