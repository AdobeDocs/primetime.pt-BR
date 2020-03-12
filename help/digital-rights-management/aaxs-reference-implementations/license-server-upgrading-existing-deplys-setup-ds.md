---
seo-title: Configurar um servidor de domínio
title: Configurar um servidor de domínio
uuid: b262ea86-f465-4ed1-b278-122d4dafc881
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurar um servidor de domínio {#set-up-a-domain-server}

Para configurar o servidor de domínio em uma instalação existente do servidor de licenças, execute as seguintes tarefas:

1. Abra o [!DNL flashaccess-refimpl.properties] arquivo em [!DNL tomcat/lib].

1. Na `Domain CA certificate` opção, preencha os detalhes do certificado da CA de domínio. Este certificado será usado para aceitar os tokens de domínio.
1. Sob a `Domain CA credential` opção, preencha os `Domain CA credential certificate (PFX)` detalhes. Este certificado será usado para assinar certificados de domínio e tokens.

1. Especifique o valor para `DomainServerlURL`. Se esse valor for NULL, a autenticação do domínio poderá ser bem-sucedida. Entretanto, ao ingressar no domínio, ocorrerá um erro de domínio de ingresso.

