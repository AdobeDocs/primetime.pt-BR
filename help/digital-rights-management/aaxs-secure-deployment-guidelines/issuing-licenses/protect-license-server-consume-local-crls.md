---
title: Consumir CRLs geradas localmente
description: Consumir CRLs geradas localmente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Consumir CRLs geradas localmente{#consume-locally-generated-crls}

Para consumir listas de revogação de certificados (CRLs) geradas localmente e listas de atualização de políticas, use APIs de acesso ao Adobe para verificar a assinatura. As APIs verificam se as listas não foram violadas e se foram assinadas pelo License Server correto.

* Chame `RevocationList.verifySignature` para verificar a assinatura antes de fornecer RevocationList a qualquer API.

   Para obter mais informações, consulte `RevocationListFactory` no *Referência da API de acesso ao Adobe*.

* Chame `PolicyUpdateList.verifySignature`para verificar a assinatura antes de fornecer `PolicyUpdateList` para qualquer API.

   Para obter mais informações, consulte `PolicyUpdateList` no *Referência da API de acesso ao Adobe*.

