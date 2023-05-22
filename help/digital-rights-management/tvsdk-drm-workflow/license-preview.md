---
title: Visualização da licença
description: Visualização da licença
copied-description: true
exl-id: 53a57610-86a8-4c5d-9494-679ede35abf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Visualização da licença {#license-preview}

Se houver uma dúvida sobre se um dispositivo pode ou não consumir e aplicar totalmente uma licença do Primetime DRM, você pode usar o recurso Visualização de licença. Uma licença de Visualização corresponde totalmente a todas as restrições e restrições definidas na licença final, mas não contém a Chave de criptografia de conteúdo (CEK) necessária para descriptografar o conteúdo protegido. Esse recurso é útil para determinar se o cliente pode realmente consumir a licença antes que o Distribuidor de conteúdo tome a decisão de fornecer uma licença específica ao cliente. Por exemplo, um cliente deseja assistir a conteúdo de alta definição, mas o Distribuidor de conteúdo deseja garantir que o dispositivo possa detectar e engajar totalmente o HDCP. Nessa situação, o cliente pode chamar `DRMManager.loadPreviewVoucher()`. Se um `DRMStatusEvent` é recebido, em vez de um `DRMErrorEvent`, então, é confirmado que o cliente pode aplicar totalmente as restrições de Proteção de saída na licença, e o Distribuidor de conteúdo pode fornecer livremente esse tipo de licença ao cliente.

[iOS acquisitionPreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[AcquisePreviewLicense() para Android](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
