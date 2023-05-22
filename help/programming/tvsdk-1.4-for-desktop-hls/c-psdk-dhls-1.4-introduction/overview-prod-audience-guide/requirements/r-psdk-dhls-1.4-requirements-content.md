---
description: Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos), incluindo chaves de criptografia DRM.
title: Requisitos de conteúdo e manifesto
exl-id: 96b2b245-558b-4606-87c0-22140430c326
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
