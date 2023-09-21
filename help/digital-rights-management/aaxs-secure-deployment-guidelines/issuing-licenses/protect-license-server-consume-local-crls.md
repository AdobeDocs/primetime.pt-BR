---
title: Consumir CRLs geradas localmente
description: Consumir CRLs geradas localmente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
