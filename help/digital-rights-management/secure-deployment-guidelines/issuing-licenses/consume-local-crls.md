---
description: Para consumir listas de revogação de certificados (CRLs) geradas localmente e listas de atualização de políticas, use as APIs de DRM do Adobe Primetime para verificar a assinatura.
title: Consumo de CRLs geradas localmente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Consumo de CRLs geradas localmente {#consuming-locally-generated-crls}

Para consumir listas de revogação de certificados (CRLs) geradas localmente e listas de atualização de políticas, use as APIs de DRM do Adobe Primetime para verificar a assinatura.

As APIs a seguir verificam se as listas não foram violadas e se as listas foram assinadas pelo License Server correto:

* Chame [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer o [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) para qualquer API.

   Para obter mais informações, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chame [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer `PolicyUpdateList` a qualquer APIs.

   Para obter mais informações, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

