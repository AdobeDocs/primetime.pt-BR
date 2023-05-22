---
title: Consumir CRLs geradas localmente
description: Consumir CRLs geradas localmente
copied-description: true
exl-id: d96418d0-8fd3-4f6d-8480-191fe540080a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Consumir CRLs geradas localmente{#consume-locally-generated-crls}

Para consumir listas de certificados revogados (CRLs) geradas localmente e listas de atualização de política, use APIs de Acesso ao Adobe para verificar a assinatura. As APIs verificam se as listas não foram adulteradas e se foram assinadas pelo License Server correto.

* Chame `RevocationList.verifySignature` para verificar a assinatura antes de fornecer a RevocationList a qualquer API.

   Para obter mais informações, consulte `RevocationListFactory` no *Referência da API de acesso do Adobe*.

* Chame `PolicyUpdateList.verifySignature`para verificar a assinatura antes de fornecer a `PolicyUpdateList` a qualquer API.

   Para obter mais informações, consulte `PolicyUpdateList` no *Referência da API de acesso do Adobe*.
