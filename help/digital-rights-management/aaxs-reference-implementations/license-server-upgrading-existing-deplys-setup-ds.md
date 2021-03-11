---
title: Configurar um servidor de domínio
description: Configurar um servidor de domínio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Configurar um servidor de domínio {#set-up-a-domain-server}

Para configurar o servidor de domínio em uma instalação existente do servidor de licenças, execute as seguintes tarefas:

1. Abra o arquivo [!DNL flashaccess-refimpl.properties] em [!DNL tomcat/lib].

1. Na opção `Domain CA certificate` , preencha os detalhes do certificado da autoridade de certificação de domínio. Este certificado será usado para aceitar os tokens de domínio.
1. Na opção `Domain CA credential` , preencha os detalhes `Domain CA credential certificate (PFX)`. Esse certificado será usado para assinar certificados de domínio e tokens.

1. Especifique o valor de `DomainServerlURL`. Se esse valor for NULL, a autenticação de domínio poderá ser bem-sucedida. No entanto, ao ingressar no domínio, haverá um erro de domínio de associação.

