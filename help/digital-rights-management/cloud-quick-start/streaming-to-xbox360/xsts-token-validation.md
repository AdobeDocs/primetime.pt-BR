---
title: Validação de token Xbox Live XSTS
description: Validação de token Xbox Live XSTS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Validação de token Xbox Live XSTS{#xbox-live-xsts-token-validation}

Para solicitações XSTS, o campo `customerSpecificAuthToken` conterá o token XSTS codificado em Base64. O código `XSTSValidator` de amostra examina o token decodificado Base64 para a existência do elemento `EncryptedAssertion`; no entanto, você pode usar outros métodos para distinguir entre essas solicitações e solicitações que não são da Xbox. Por exemplo, você pode usar um URL diferente.

A política retornada na mensagem de resposta substituirá a política original nos metadados DRM fornecidos com a solicitação da chave Xbox. Somente um subconjunto de recursos de política é suportado pelo cliente Xbox, e esses campos são os únicos que substituirão a política original.

Há etapas de configuração adicionais necessárias para oferecer suporte à descriptografia e validação de token. Você deve carregar as credenciais [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] em um armazenamento de chaves do formato JKS, que você fornece ao servidor de direito de back-end como a propriedade de sistema `xsts-keystore`. Por padrão, o parceiro [!DNL .pfx] tem o alias `xsts` e o certificado de validação do token tem o alias `xsts-verify-cert`. Também é possível substituí-los usando as propriedades do sistema. Finalmente, há uma propriedade do sistema `xsts-keystore-password` que não tem o padrão e que contém a senha do armazenamento de chaves. As propriedades do sistema lidas pelo código `XSTSValidator` são resumidas abaixo:

| Propriedade do sistema | Valor padrão | Comentário |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Armazenamento de chaves do formato JKS usado pelo validador. |
| `xsts-keystore-password` |  | Senha do repositório de chaves |
| `xsts-alias` | `xsts` | Alias usado para recuperar a chave de descriptografia do repositório de chaves |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias usado para recuperar o certificado de validação do repositório de chaves |

