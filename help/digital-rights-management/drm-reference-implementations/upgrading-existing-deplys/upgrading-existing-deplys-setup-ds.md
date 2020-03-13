---
description: nulo
seo-description: nulo
seo-title: Configurar um servidor de domínio
title: Configurar um servidor de domínio
uuid: bf85305e-9a00-4bc0-ba36-c870979456e4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurar um servidor de domínio{#set-up-a-domain-server}

Para configurar um servidor de domínio em uma instalação existente do servidor de licenças:

1. No [!DNL tomcat/lib] diretório, abra o [!DNL flashaccess-refimpl.properties] arquivo.
1. Na `Domain CA certificate` opção, preencha o certificado da CA de domínio.

   Esse certificado é usado para aceitar os tokens de domínio.
1. Na `Domain CA credential` opção, preencha os `Domain CA credential certificate (PFX)` detalhes.

   Esse certificado é usado para assinar certificados de domínio e tokens.
1. Especifique o valor para `DomainServerlURL`.

   Se esse valor for definido como `NULL`, a autenticação do domínio poderá ser bem-sucedida. Entretanto, ao ingressar no domínio, um erro de domínio de ingresso pode ocorrer.
