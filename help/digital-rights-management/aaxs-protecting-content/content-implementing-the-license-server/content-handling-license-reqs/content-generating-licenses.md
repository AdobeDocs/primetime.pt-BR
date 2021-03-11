---
title: Geração de licenças
description: Geração de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Gerar licenças {#generating-licenses}

Para emitir uma licença de folha para o usuário, o SDK deve descriptografar o CEK contido nos metadados do conteúdo e criptografá-lo novamente para o computador que solicita uma licença. Para descriptografar o CEK, o servidor deve fornecer as informações necessárias para descriptografar a chave. Chame `ContentInfo.setKeyRetrievalInfo()` e forneça um objeto `AsymmetricKeyRetrieval`. Se os metadados contiverem várias políticas, o servidor deverá determinar qual política usar e chamar `LicenseRequestMessage.setSelectedPolicy()`. Em seguida, chame `LicenseRequestMessage.generateLicense()` para gerar a licença. Usando o objeto `License` retornado, você pode modificar a expiração ou os direitos na licença.

Se um objeto ExternalKeyRetrieval for especificado no objeto `ContentInfo` , o servidor de licenças deve usar a ID CEK associada para buscar o CEK apropriado que será inserido na licença. Para obter mais detalhes sobre como usar o workflow CEK externo, consulte [Visão geral externa do CEK do DRM de acesso ao Adobe](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
