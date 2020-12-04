---
seo-title: Como incorporar licenças
title: Como incorporar licenças
uuid: e3d55376-07de-479c-9a53-04bc8071ced4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Como incorporar licenças {#embedding-licenses}

Depois que o conteúdo é criptografado e uma licença é gerada previamente, a licença pode ser incorporada ao conteúdo criptografado.

Se você quiser incorporar uma licença, é necessário obter uma instância de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se você souber o tipo de conteúdo criptografado, use o construtor para `FLVKeyMetaDataUpdater` ou `F4VKeyMetaDataUpdater`; caso contrário, use `MediaProcessorFactory.getMediaProcessor()` para retornar uma instância com base no tipo de arquivo detectado. Em seguida, é necessário construir um `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. Sua implementação de retorno de chamada é então chamada quando os metadados DRM estão localizados no conteúdo criptografado. Com base nos metadados encontrados, você pode escolher uma licença para incorporar e definir a licença usando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` no diretório Reference Implementation Command Line Tools [!DNL Samples] para obter exemplos de códigos que demonstram licenças incorporadas.

>[!NOTE]
>
>Um cliente Adobe Primetime DRM 2.0 ignora todas as licenças incorporadas ao conteúdo e tenta obter uma licença do servidor de licença especificado nos metadados. No entanto, se os metadados indicarem que nenhum servidor de licença está disponível, um cliente Primetime DRM 2.0 precisa ser atualizado antes que você possa visualização do conteúdo.

