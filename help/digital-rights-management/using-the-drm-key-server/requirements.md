---
seo-title: Requisitos para o uso do servidor de chave DRM Primetime
title: Requisitos para o uso do servidor de chave DRM Primetime
uuid: 769f9e10-7a3e-4a38-b30d-18181b666bb4
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Introdução {#introduction}

O Primetime DRM Key Server é um servidor de chaves de vários locatários para a entrega de chaves Remotas iOS e/ou Xbox 360. Se a Entrega de chave remota estiver ativada em uma política para iOS, um Servidor de chave DRM Primetime deverá ser implantado para permitir a reprodução de conteúdo em clientes iOS. O Primetime DRM Key Server é sempre necessário para o Xbox 360.

## Requisitos para o uso do servidor de chave DRM Primetime {#requirements-for-using-primetime-drm-key-server}

Os requisitos mínimos para usar o Primetime DRM Key Server são:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) ou posterior. (Para usar o HSM no Windows de 64 bits, é necessário o JRE 8)

   >[!NOTE]
   >
   >O PKCS11 de 64 bits agora é compatível com o OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131)e Oracle JDK: [https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6880559).

* [Apache Tomcat 7](https://tomcat.apache.org)
* Credenciais emitidas pela Adobe
* Credenciais emitidas pela Microsoft (para clientes Xbox 360)