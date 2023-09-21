---
title: Gerando licenças
description: Gerando licenças
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Gerando licenças{#generating-licenses}

Se você quiser emitir uma licença folha para um usuário, o SDK deverá descriptografar o CEK contido nos metadados de conteúdo e criptografá-lo novamente para o computador que solicita uma licença. Para descriptografar o CEK, o servidor deve fornecer as informações necessárias para descriptografar a chave. Chame `ContentInfo.setKeyRetrievalInfo()` e fornecer uma `AsymmetricKeyRetrieval` objeto. Se os metadados incluírem várias políticas, o servidor deverá determinar qual política usar e chamar `LicenseRequestMessage.setSelectedPolicy()`. Em seguida, chame `LicenseRequestMessage.generateLicense()` para gerar a licença. Usar o `License` que é retornado, você pode modificar a expiração ou os direitos na licença.

Se um `ExternalKeyRetrieval` objeto é especificado na variável `ContentInfo` , o servidor de licenças deverá usar a ID do CEK associada para recuperar o CEK apropriado inserido na licença.

Consulte a [Visão geral do CEK externo do Adobe Primetime DRM](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) para obter mais detalhes sobre como usar o workflow externo do CEK.
