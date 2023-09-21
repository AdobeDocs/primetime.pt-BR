---
title: Configurar um servidor de domínio
description: Configurar um servidor de domínio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# Configurar um servidor de domínio{#set-up-a-domain-server}

Para configurar um servidor de domínio em uma instalação existente do servidor de licenças:

1. No [!DNL tomcat/lib] , abra o [!DNL flashaccess-refimpl.properties] arquivo.
1. No `Domain CA certificate` opção, preencha o certificado de CA de domínio.

   Esse certificado é usado para aceitar os tokens de domínio.
1. No `Domain CA credential` opção, conclua o `Domain CA credential certificate (PFX)` detalhes.

   Esse certificado é usado para assinar certificados de domínio e tokens.
1. Especifique o valor para `DomainServerlURL`.

   Se esse valor estiver definido como `NULL`, a autenticação do domínio poderá ser bem-sucedida. No entanto, ao ingressar no domínio, pode ocorrer um erro.
