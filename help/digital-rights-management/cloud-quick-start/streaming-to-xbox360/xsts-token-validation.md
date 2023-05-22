---
title: Validação de token XSTS do Xbox Live
description: Validação de token XSTS do Xbox Live
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Validação de token XSTS do Xbox Live{#xbox-live-xsts-token-validation}

Para solicitações XSTS, a variável `customerSpecificAuthToken` conterá o token XSTS codificado na Base64. A amostra `XSTSValidator` O código examina o token decodificado Base64 para a existência do `EncryptedAssertion` elemento; no entanto, você pode usar outros métodos para distinguir entre essas solicitações e solicitações que não são do Xbox. Por exemplo, você pode usar um URL diferente.

A política retornada na mensagem de resposta substituirá a política original nos metadados DRM fornecidos com a solicitação de chave do Xbox. Somente um subconjunto de recursos de política é suportado pelo cliente Xbox, e esses campos são os únicos que substituirão a política original.

Há etapas de configuração adicionais necessárias para oferecer suporte à descriptografia e validação de tokens. Você deve carregar o [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] em um armazenamento de chaves no formato JKS, que você fornece ao servidor de direitos de back-end como a propriedade do sistema `xsts-keystore`. Por padrão, o parceiro [!DNL .pfx] tem o alias `xsts`e o certificado de validação de token tem o alias `xsts-verify-cert`. Também é possível substituí-los usando propriedades do sistema. Finalmente, há uma propriedade do sistema `xsts-keystore-password` que não tem padrão e que contém a senha do keystore. As propriedades do sistema lidas pelo `XSTSValidator` estão resumidos abaixo:

| Propriedade do sistema | Valor padrão | Comentário |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Armazenamento de chaves no formato JKS usado pelo validador. |
| `xsts-keystore-password` |  | Senha para o keystore |
| `xsts-alias` | `xsts` | Alias usado para recuperar a chave de descriptografia do keystore |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias usado para recuperar o certificado de validação do armazenamento de chaves |

