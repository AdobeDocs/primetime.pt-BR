---
seo-title: Gerando licenças
title: Gerando licenças
uuid: 242d5567-f609-4781-a8a6-2f3d78471344
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Gerando licenças {#generating-licenses}

Para emitir uma licença de folha para o usuário, o SDK deve descriptografar o CEK contido nos metadados do conteúdo e criptografá-lo novamente para o computador que solicita uma licença. Para descriptografar o CEK, o servidor deve fornecer as informações necessárias para descriptografar a chave. Chame `ContentInfo.setKeyRetrievalInfo()` e forneça um objeto `AsymmetricKeyRetrieval`. Se os metadados contiverem várias políticas, o servidor deverá determinar qual política usar e chamar `LicenseRequestMessage.setSelectedPolicy()`. Em seguida, chame `LicenseRequestMessage.generateLicense()` para gerar a licença. Usando o objeto `License` que é retornado, você pode modificar a expiração ou os direitos na licença.

Se um objeto ExternalKeyRetrieval for especificado no objeto `ContentInfo`, o servidor de licenças deverá usar a ID CEK associada para buscar o CEK apropriado que será inserido na licença. Para obter mais detalhes sobre como usar o fluxo de trabalho CEK externo, consulte [Visão geral do CEK externo do DRM de acesso ao Adobe](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
