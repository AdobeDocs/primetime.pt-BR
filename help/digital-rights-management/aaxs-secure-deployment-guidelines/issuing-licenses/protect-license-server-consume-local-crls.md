---
seo-title: Consumir CRLs geradas localmente
title: Consumir CRLs geradas localmente
uuid: 5a4519b8-6dbd-4921-9048-6c9f67aae18d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Consumir CRLs geradas localmente{#consume-locally-generated-crls}

Para consumir listas de revogação de certificado (CRLs) geradas localmente e listas de atualização de política, use as APIs de acesso ao Adobe para verificar a assinatura. As APIs verificam se as listas não foram adulteradas e se foram assinadas pelo License Server correto.

* Chame `RevocationList.verifySignature` para verificar a assinatura antes de fornecer a RevocationList a qualquer APIs.

   Para obter mais informações, consulte `RevocationListFactory` na *Referência da API de acesso ao Adobe*.

* Chame `PolicyUpdateList.verifySignature`para verificar a assinatura antes de fornecer `PolicyUpdateList` para qualquer API.

   Para obter mais informações, consulte `PolicyUpdateList` na *Referência da API de acesso ao Adobe*.

