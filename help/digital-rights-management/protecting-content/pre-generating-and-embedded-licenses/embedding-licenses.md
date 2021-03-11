---
title: Como incorporar licenças
description: Como incorporar licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Como incorporar licenças {#embedding-licenses}

Depois que o conteúdo for criptografado e uma licença tiver sido pré-gerada, ela poderá ser incorporada ao conteúdo criptografado.

Se quiser incorporar uma licença, você precisa obter uma instância de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se você sabe o tipo de conteúdo criptografado, use o construtor para `FLVKeyMetaDataUpdater` ou `F4VKeyMetaDataUpdater`; caso contrário, use `MediaProcessorFactory.getMediaProcessor()` para retornar uma instância com base no tipo de arquivo detectado. Em seguida, é necessário construir um `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. Sua implementação de retorno de chamada é então invocada quando os metadados de DRM estão localizados no conteúdo criptografado. Com base nos metadados encontrados, você pode escolher uma licença para incorporar e definir a licença usando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` no diretório Ferramentas de linha de comando da implementação de referência [!DNL Samples] para obter o código de amostra que demonstra licenças incorporadas.

>[!NOTE]
>
>Um cliente Adobe Primetime DRM 2.0 ignora qualquer licença incorporada ao conteúdo e, em seguida, tenta obter uma licença do servidor de licença especificado nos metadados. No entanto, se os metadados indicarem que nenhum servidor de licença está disponível, um cliente DRM 2.0 do Primetime precisa ser atualizado antes que você possa exibir o conteúdo.

