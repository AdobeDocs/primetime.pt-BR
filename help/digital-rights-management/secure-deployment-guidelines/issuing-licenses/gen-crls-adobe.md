---
description: Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pelo Adobe.
title: Geração de CRLs para complementar os publicados pelo Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Geração de CRLs para complementar aqueles publicados pelo Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pelo Adobe.

O SDK de DRM do Primetime verifica e aplica as CRLs do Adobe. No entanto, você pode não permitir máquinas cliente adicionais criando uma CRL que revoga credenciais de máquina adicionais transmitindo a CRL para o SDK de DRM do Primetime. Ao emitir uma licença, o SDK verifica a CRL do Adobe e a CRL.

Para gerar CRLs, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
