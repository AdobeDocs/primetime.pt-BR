---
title: Como incorporar licenças
description: Como incorporar licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Como incorporar licenças {#embedding-licenses}

Depois que o conteúdo for criptografado e uma licença tiver sido pré-gerada, ela poderá ser incorporada ao conteúdo criptografado.

Para incorporar uma licença, obtenha uma instância de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se você sabe o tipo de conteúdo criptografado, use o construtor para `FLVKeyMetaDataUpdater` ou `F4VKeyMetaDataUpdater`; caso contrário, use `MediaProcessorFactory.getMediaProcessor()` para retornar uma instância com base no tipo de arquivo detectado. Construa um `KeyMetaDataCallback` e chame `modifyKeyMetaData()`. Sua implementação de retorno de chamada será invocada quando os metadados de DRM estiverem localizados no conteúdo criptografado. Com base nos metadados encontrados, você pode escolher uma licença para incorporar e definir a licença usando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Para obter um código de amostra demonstrando licenças incorporadas, consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` no diretório &quot;Samples&quot; das Ferramentas de linha de comando de implementação de referência.

>[!NOTE]
>
>Os clientes do Adobe Access 2.0 ignorarão quaisquer licenças incorporadas no conteúdo e tentarão obter uma licença do servidor de licenças especificado nos metadados. No entanto, se os metadados indicarem que nenhum servidor de licença está disponível, um cliente do Adobe Access 2.0 precisará atualizar para visualizar o conteúdo.

Consulte [Licenças fora de banda](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
