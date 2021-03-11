---
title: Visualização da licença
description: Visualização da licença
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Visualização da licença {#license-preview}

Se houver uma dúvida sobre se um dispositivo pode consumir e aplicar totalmente uma licença de DRM do Primetime, você poderá usar o recurso de Visualização de licença. Uma licença de Visualização corresponde totalmente a todas as restrições e restrições definidas na licença final, mas não contém a Chave de criptografia de conteúdo (CEK) necessária para descriptografar o conteúdo protegido. Esse recurso é útil para determinar se o cliente pode realmente consumir a licença antes que o Distribuidor de conteúdo tome a decisão de fornecer uma licença específica ao cliente. Por exemplo - um cliente deseja assistir ao conteúdo de alta definição, mas o Distribuidor de conteúdo quer garantir que o dispositivo possa detectar e engajar totalmente o HDCP. Nessa situação, o cliente pode chamar `DRMManager.loadPreviewVoucher()`. Se um `DRMStatusEvent` for recebido, em vez de um `DRMErrorEvent`, confirma-se que o cliente pode aplicar totalmente as restrições de Proteção de Saída na licença e o Distribuidor de Conteúdo pode fornecer livremente esse tipo de licença ao cliente.

[iOS acquisitionPreviewLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a3baac603bdd8826624dbe97f9faaba10)

[Android acquisitionPreviewLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquirePreviewLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))
