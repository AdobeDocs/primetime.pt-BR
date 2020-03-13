---
description: Para consumir listas de revogação de certificados (CRLs) e listas de atualização de políticas geradas localmente, use as APIs DRM do Adobe Primetime para verificar a assinatura.
seo-description: Para consumir listas de revogação de certificados (CRLs) e listas de atualização de políticas geradas localmente, use as APIs DRM do Adobe Primetime para verificar a assinatura.
seo-title: Consumir CRLs geradas localmente
title: Consumir CRLs geradas localmente
uuid: 2e20b8ca-8606-4c27-b585-2f020b93be32
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Consumir CRLs geradas localmente {#consuming-locally-generated-crls}

Para consumir listas de revogação de certificados (CRLs) e listas de atualização de políticas geradas localmente, use as APIs DRM do Adobe Primetime para verificar a assinatura.

As APIs a seguir verificam se as listas não foram adulteradas e se as listas foram assinadas pelo License Server correto:

* Chame [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer a [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualquer API.

   Para obter mais informações, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chame [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer a `PolicyUpdateList` APIs.

   Para obter mais informações, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

