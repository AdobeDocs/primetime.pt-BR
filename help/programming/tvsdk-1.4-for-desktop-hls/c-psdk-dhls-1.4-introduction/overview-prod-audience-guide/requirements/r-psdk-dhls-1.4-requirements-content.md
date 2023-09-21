---
description: Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos), incluindo chaves de criptografia DRM.
title: Requisitos de conteúdo e manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Requisitos de conteúdo e manifesto {#content-and-manifest-requirements}

Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos), incluindo chaves de criptografia DRM.

| Incluir e definir o `RESOLUTION` para cada fluxo ABR no arquivo de manifesto. Você deve usar o Flash Player 14 ou posterior. |
|---|
| Se o fluxo protegido por DRM for MBR (multiple bit rate), a chave de criptografia DRM usada para o MBR deve ser a mesma que a chave usada em todos os fluxos de taxa de bits. |
| Deve ter as mesmas representações de taxa de bits que as representações do conteúdo principal. |
