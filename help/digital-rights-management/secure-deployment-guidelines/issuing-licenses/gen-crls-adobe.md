---
description: Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pelo Adobe.
title: Gerar CRLs para complementar aquelas publicadas pelo Adobe
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Gerar CRLs para complementar aquelas publicadas pelo Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pelo Adobe.

O SDK do DRM do Primetime verifica e impõe as CRLs de Adobe. No entanto, você pode não permitir máquinas clientes adicionais criando uma CRL que revogue credenciais de máquina adicionais transmitindo a CRL para o SDK DRM do Primetime. Quando você emite uma licença, o SDK verifica a CRL do Adobe e a CRL.

Para gerar CRLs, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
