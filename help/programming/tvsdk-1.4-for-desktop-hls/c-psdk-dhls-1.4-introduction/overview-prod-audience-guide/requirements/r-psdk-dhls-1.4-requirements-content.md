---
description: Verifique as restrições e os requisitos para streams e playlists (manifestos), incluindo chaves de criptografia DRM.
seo-description: Verifique as restrições e os requisitos para streams e playlists (manifestos), incluindo chaves de criptografia DRM.
seo-title: Requisitos de conteúdo e manifesto
title: Requisitos de conteúdo e manifesto
uuid: 53cc570a-be33-4488-95e8-43f91b559b13
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# Requisitos de conteúdo e manifesto {#content-and-manifest-requirements}

Verifique as restrições e os requisitos para streams e playlists (manifestos), incluindo chaves de criptografia DRM.

| Inclua e defina a propriedade `RESOLUTION` para cada fluxo ABR no arquivo manifest. Você deve usar o Flash Player 14 ou posterior. |
|---|
| Se o fluxo protegido por DRM for uma taxa de bits múltipla (MBR), a chave de criptografia de DRM usada para o MBR deve ser a mesma usada em todos os fluxos de taxa de bits. |
| Deve ter as mesmas execuções de taxa de bits que as execuções do conteúdo principal. |