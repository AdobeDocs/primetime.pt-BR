---
description: Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL do computador publicada pelo Adobe.
seo-description: Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL do computador publicada pelo Adobe.
seo-title: Geração de LCRs para complementar os publicados pela Adobe
title: Geração de LCRs para complementar os publicados pela Adobe
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# Geração de CRLs para complementar os publicados por Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL do computador publicada pelo Adobe.

O Primetime DRM SDK verifica e aplica as CRLs de Adobe. No entanto, você pode proibir computadores clientes adicionais criando uma CRL que revogue credenciais adicionais do computador transmitindo a CRL para o SDK do DRM Primetime. Quando você emite uma licença, o SDK verifica a CRL Adobe e a CRL.

Para gerar CRLs, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
