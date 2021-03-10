---
title: Configurar um servidor de domínio
description: Configurar um servidor de domínio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---


# Configurar um servidor de domínio{#set-up-a-domain-server}

Para configurar um servidor de domínio em uma instalação existente do servidor de licenças:

1. No diretório [!DNL tomcat/lib], abra o arquivo [!DNL flashaccess-refimpl.properties].
1. Na opção `Domain CA certificate`, preencha o certificado de autoridade de certificação de domínio.

   Esse certificado é usado para aceitar os tokens de domínio.
1. Na opção `Domain CA credential`, preencha os detalhes `Domain CA credential certificate (PFX)`.

   Esse certificado é usado para assinar certificados de domínio e tokens.
1. Especifique o valor de `DomainServerlURL`.

   Se esse valor for definido como `NULL`, a autenticação de domínio poderá ser bem-sucedida. No entanto, ao ingressar no domínio, um erro de domínio de associação pode ocorrer.
