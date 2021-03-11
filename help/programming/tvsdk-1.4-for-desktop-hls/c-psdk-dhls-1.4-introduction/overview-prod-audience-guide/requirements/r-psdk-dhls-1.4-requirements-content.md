---
description: Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos), incluindo chaves de criptografia de DRM.
title: Requisitos de conteúdo e manifesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# Requisitos de conteúdo e manifesto {#content-and-manifest-requirements}

Verifique as restrições e os requisitos para fluxos e listas de reprodução (manifestos), incluindo chaves de criptografia de DRM.

| Inclua e defina a propriedade `RESOLUTION` para cada fluxo ABR no arquivo de manifesto. Você deve usar o Flash Player 14 ou posterior. |
|---|
| Se o fluxo protegido por DRM for de taxa múltipla de bits (MBR), a chave de criptografia de DRM usada para o MBR deverá ser a mesma usada em todos os fluxos de taxa de bits. |
| Deve ter as mesmas representações de taxa de bits que as representações do conteúdo principal. |