---
title: Incorporação de licenças
description: Incorporação de licenças
copied-description: true
exl-id: 63b1bf18-b93d-4305-885a-3a9eee783a03
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Incorporação de licenças {#embedding-licenses}

Depois que o conteúdo é criptografado e uma licença é pré-gerada, a licença pode ser incorporada ao conteúdo criptografado.

Para incorporar uma licença, obtenha uma instância de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se você souber o tipo do conteúdo criptografado, use o construtor para `FLVKeyMetaDataUpdater` ou `F4VKeyMetaDataUpdater`; caso contrário, use `MediaProcessorFactory.getMediaProcessor()` para retornar uma instância com base no tipo de arquivo detectado. Construir um `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. Sua implementação de retorno de chamada será invocada quando os metadados de DRM estiverem localizados no conteúdo criptografado. Com base nos metadados encontrados, você pode escolher uma licença para incorporar e definir a licença usando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Para obter exemplos de código demonstrando licenças incorporadas, consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` no diretório &quot;Amostras&quot; de Ferramentas de Linha de Comando de Implementação de Referência.

>[!NOTE]
>
>Os clientes do Adobe Access 2.0 ignorarão todas as licenças incorporadas ao conteúdo e tentarão obter uma licença do servidor de licenças especificado nos metadados. No entanto, se os metadados indicarem que não há servidor de licenças disponível, um cliente do Adobe Access 2.0 precisará ser atualizado para visualizar o conteúdo.

Consulte [Licenças fora da banda](../../aaxs-protecting-content/content-introduction/packaging-options/content-out-of-band-licenses.md).
