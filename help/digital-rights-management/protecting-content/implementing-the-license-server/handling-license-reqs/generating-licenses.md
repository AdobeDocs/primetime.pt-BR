---
seo-title: Gerando licenças
title: Gerando licenças
uuid: f91b0cc8-e0ed-4722-947b-22eb2bfba916
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Gerando licenças{#generating-licenses}

Se você quiser emitir uma licença de folha para um usuário, o SDK deverá descriptografar o CEK contido nos metadados do conteúdo e criptografá-lo novamente para o computador que solicita uma licença. Para descriptografar o CEK, o servidor deve fornecer as informações necessárias para descriptografar a chave. Chame `ContentInfo.setKeyRetrievalInfo()` e forneça um `AsymmetricKeyRetrieval` objeto. Se os metadados incluírem várias políticas, o servidor deverá determinar qual política usar e chamar `LicenseRequestMessage.setSelectedPolicy()`. Em seguida, chame `LicenseRequestMessage.generateLicense()` para gerar a licença. Usando o `License` objeto retornado, você pode modificar a expiração ou os direitos na licença.

Se um `ExternalKeyRetrieval` objeto for especificado no `ContentInfo` objeto, o servidor de licenças deve usar a ID CEK associada para recuperar o CEK apropriado inserido na licença.

Consulte a Visão geral [do CEK externo do DRM do](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) Adobe Primetime para obter mais detalhes sobre como usar o fluxo de trabalho do CEK externo.
