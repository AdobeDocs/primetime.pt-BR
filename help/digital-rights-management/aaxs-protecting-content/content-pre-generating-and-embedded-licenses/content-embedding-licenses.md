---
seo-title: Como incorporar licenças
title: Como incorporar licenças
uuid: b8d8ee9b-7430-4899-9caf-47d6b64021b8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Como incorporar licenças {#embedding-licenses}

Depois que o conteúdo é criptografado e uma licença é gerada previamente, a licença pode ser incorporada ao conteúdo criptografado.

Para incorporar uma licença, obtenha uma instância de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se você souber o tipo de conteúdo criptografado, use o construtor para `FLVKeyMetaDataUpdater` ou `F4VKeyMetaDataUpdater`; caso contrário, use `MediaProcessorFactory.getMediaProcessor()` para retornar uma instância com base no tipo de arquivo detectado. Construa um `KeyMetaDataCallback` e chame `modifyKeyMetaData()`. Sua implementação de retorno de chamada será invocada quando os metadados do DRM estiverem localizados no conteúdo criptografado. Com base nos metadados encontrados, você pode escolher uma licença para incorporar e definir a licença usando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Para obter exemplos de códigos que demonstram licenças incorporadas, consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` o diretório &quot;Amostras&quot; das Ferramentas de Linha de Comando de Implementação de Referência.

>[!NOTE]
>
>Os clientes do Adobe Access 2.0 ignorarão quaisquer licenças incorporadas no conteúdo e tentarão obter uma licença do servidor de licenças especificado nos metadados. No entanto, se os metadados indicarem que nenhum servidor de licença está disponível, um cliente do Adobe Access 2.0 precisará atualizar para visualização do conteúdo.

Consulte Licenças [fora da banda](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
