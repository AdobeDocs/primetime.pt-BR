---
seo-title: Pré-visualização de licença
title: Pré-visualização de licença
uuid: 61ff171f-b977-40ef-8e8d-2900316fa89a
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Pré-visualização de licença {#license-preview}

Se houver uma dúvida sobre se um dispositivo pode consumir ou não e aplicar totalmente uma licença de DRM Primetime, você pode usar o recurso Pré-visualização de licença. Uma licença de Pré-visualização corresponde a todas as restrições e restrições definidas na licença final, mas não contém a Chave de criptografia de conteúdo (CEK) necessária para descriptografar o conteúdo protegido. Esse recurso é útil para determinar se o cliente pode realmente consumir a licença antes que o Distribuidor de conteúdo tome a decisão de fornecer uma licença específica ao cliente. Por exemplo: um cliente deseja assistir a conteúdo HD, mas o Distribuidor de conteúdo quer garantir que o dispositivo possa detectar e acionar o HDCP completamente. Nessa situação, o cliente pode chamar `DRMManager.loadPreviewVoucher()`. Se um `DRMStatusEvent` for recebido, em vez de um `DRMErrorEvent`, será confirmado que o cliente pode aplicar totalmente as restrições de Proteção de Saída na licença, e o Distribuidor de Conteúdo pode fornecer livremente esse tipo de licença ao cliente.

[iOS acquisitionPreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquisitionPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
