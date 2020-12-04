---
seo-title: Validação de token Xbox Live XSTS
title: Validação de token Xbox Live XSTS
uuid: 9647f8ee-32d6-4bed-bae2-8b36a72d04ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Validação do token Xbox Live XSTS{#xbox-live-xsts-token-validation}

Para solicitações XSTS, o campo `customerSpecificAuthToken` conterá o token XSTS codificado em Base64. O código de amostra `XSTSValidator` examina o token decodificado Base64 quanto à existência do elemento `EncryptedAssertion`; no entanto, você pode usar outros métodos para distinguir entre essas solicitações e solicitações que não sejam do Xbox. Por exemplo, você pode usar um URL diferente.

A política retornada na mensagem de resposta substituirá a política original nos metadados DRM fornecidos com a solicitação de chave Xbox. Somente um subconjunto de recursos de política é suportado pelo cliente Xbox e esses campos são os únicos que substituirão a política original.

Existem etapas de configuração adicionais necessárias para suportar a decodificação e validação de token. Você deve carregar as credenciais [!DNL xsts_partner_cert.pfx] e [!DNL x_secure_token_service.part.xboxlive.com.cer] em um armazenamento de chave no formato JKS, que você fornece ao servidor de direito de back-end como a propriedade do sistema `xsts-keystore`. Por padrão, o parceiro [!DNL .pfx] tem o alias `xsts` e o certificado de validação do token tem o alias `xsts-verify-cert`. Também é possível substituí-los usando as propriedades do sistema. Finalmente, há uma propriedade do sistema `xsts-keystore-password` que não tem padrão e que contém a senha do armazenamento de chaves. As propriedades do sistema lidas pelo código `XSTSValidator` são resumidas abaixo:

| Propriedade do sistema | Valor padrão | Comentário |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | Armazenamento de chave no formato JKS usado pelo validador. |
| `xsts-keystore-password` |  | Senha para o armazenamento de chaves |
| `xsts-alias` | `xsts` | Alias usado para recuperar a chave de decodificação do armazenamento de chaves |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | Alias usado para recuperar o certificado de validação do armazenamento de chaves |

