---
title: Configurar um servidor de domínio
description: Configurar um servidor de domínio
copied-description: true
exl-id: b2589412-25e4-44c8-be11-8b2cfccbf7bb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Configurar um servidor de domínio {#set-up-a-domain-server}

Para configurar o servidor de domínio em uma instalação existente do servidor de licenças, execute as seguintes tarefas:

1. Abra o [!DNL flashaccess-refimpl.properties] arquivo em [!DNL tomcat/lib].

1. No `Domain CA certificate` opção, preencha os detalhes do certificado de CA de domínio. Este certificado será usado para aceitar os tokens de domínio.
1. No `Domain CA credential` opção, preencha o `Domain CA credential certificate (PFX)` detalhes. Este certificado será usado para assinar certificados de domínio e tokens.

1. Especifique o valor para `DomainServerlURL`. Se esse valor for NULL, a autenticação do domínio poderá ser bem-sucedida. No entanto, ao ingressar no domínio, haverá um erro de ingresso no domínio.
