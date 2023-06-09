---
title: Requisitos para usar o servidor de chaves DRM do Primetime
description: Requisitos para usar o servidor de chaves DRM do Primetime
copied-description: true
exl-id: a5c0db05-15a1-45b0-abb9-11f857f5e34c
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Introdução {#introduction}

O servidor de chaves DRM do Primetime é um servidor de chaves de vários locatários para entrega remota de chaves iOS e/ou Xbox 360. Se a Entrega remota de chave estiver habilitada em uma política para o iOS, um Servidor de chave DRM do Primetime deverá ser implantado para habilitar a reprodução de conteúdo em clientes iOS. O Servidor de Chave DRM do Primetime é sempre necessário para o Xbox 360.

## Requisitos para usar o servidor de chaves DRM do Primetime {#requirements-for-using-primetime-drm-key-server}

Os requisitos mínimos para usar o Servidor de Chaves DRM do Primetime são:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) ou posteriormente. (Para usar o HSM no Windows de 64 bits, é necessário o JRE 8)

  >[!NOTE]
  >
  >O PKCS11 de 64 bits agora é suportado no OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131), e ORACLE
* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenciais emitidas pelo Adobe
* Credenciais emitidas pelo Microsoft (para clientes Xbox 360)
