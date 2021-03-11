---
title: Requisitos para usar o servidor de chaves DRM do Primetime
description: Requisitos para usar o servidor de chaves DRM do Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Introdução {#introduction}

O Primetime DRM Key Server é um servidor de chaves de vários locatários para entrega remota de chaves iOS e/ou Xbox 360. Se a Entrega de Chave Remota estiver ativada em uma política para iOS, um Servidor de Chave DRM Primetime deverá ser implantado para habilitar a reprodução de conteúdo em clientes iOS. O servidor de chaves DRM do Primetime é sempre necessário para o Xbox 360.

## Requisitos para usar o servidor de chaves DRM do Primetime {#requirements-for-using-primetime-drm-key-server}

Os requisitos mínimos para usar o Primetime DRM Key Server são:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) ou posterior. (Para usar o HSM no Windows 64 bits, é necessário JRE 8)

   >[!NOTE]
   >
   >O PKCS11 de 64 bits agora é compatível com o OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131) e Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenciais emitidas pelo Adobe
* Credenciais emitidas pela Microsoft (para clientes Xbox 360)