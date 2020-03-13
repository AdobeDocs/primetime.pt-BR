---
description: Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pela Adobe.
seo-description: Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pela Adobe.
seo-title: Geração de CRLs para complementar as publicadas pela Adobe
title: Geração de CRLs para complementar as publicadas pela Adobe
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Geração de CRLs para complementar as publicadas pela Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pela Adobe.

O Primetime DRM SDK verifica e aplica as CRLs da Adobe. No entanto, você pode proibir computadores clientes adicionais criando uma CRL que revogue credenciais adicionais do computador transmitindo a CRL para o SDK do DRM Primetime. Quando você emite uma licença, o SDK verifica a Adobe CRL e sua CRL.

Para gerar CRLs, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
