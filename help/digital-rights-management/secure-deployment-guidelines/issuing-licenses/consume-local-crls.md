---
description: Para consumir listas de revogação de certificado (CRLs) geradas localmente e listas de atualização de política, use as APIs DRM da Adobe Primetime para verificar a assinatura.
seo-description: Para consumir listas de revogação de certificado (CRLs) geradas localmente e listas de atualização de política, use as APIs DRM da Adobe Primetime para verificar a assinatura.
seo-title: Consumir CRLs geradas localmente
title: Consumir CRLs geradas localmente
uuid: 2e20b8ca-8606-4c27-b585-2f020b93be32
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---


# Consumir CRLs geradas localmente {#consuming-locally-generated-crls}

Para consumir listas de revogação de certificado (CRLs) geradas localmente e listas de atualização de política, use as APIs DRM da Adobe Primetime para verificar a assinatura.

As APIs a seguir verificam se as listas não foram adulteradas e se as listas foram assinadas pelo License Server correto:

* Chame [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualquer APIs.

   Para obter mais informações, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chame [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer `PolicyUpdateList` para qualquer API.

   Para obter mais informações, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

