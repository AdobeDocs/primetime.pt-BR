---
title: Incorporação de licenças
description: Incorporação de licenças
copied-description: true
exl-id: 8cd58808-73fb-4635-9a75-0520430f6b3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Incorporação de licenças {#embedding-licenses}

Depois que o conteúdo é criptografado e uma licença é pré-gerada, a licença pode ser incorporada ao conteúdo criptografado.

Se quiser incorporar uma licença do, obtenha uma instância de `com.adobe.flashaccess.sdk.media.drm.contentupdate.MediaKeyMetaDataUpdater`. Se você souber o tipo do conteúdo criptografado, use o construtor para `FLVKeyMetaDataUpdater` ou `F4VKeyMetaDataUpdater`; caso contrário, use `MediaProcessorFactory.getMediaProcessor()` para retornar uma instância com base no tipo de arquivo detectado. Em seguida, é necessário construir um `KeyMetaDataCallback` e invocar `modifyKeyMetaData()`. A implementação de retorno de chamada é invocada quando os metadados de DRM estão localizados no conteúdo criptografado. Com base nos metadados encontrados, você pode escolher uma licença para incorporar e definir a licença usando `EmbedLicenseKeyMetaData.setEmbeddedLicenses()`.

Consulte `com.adobe.flashaccess.samples.licenseembedder.EmbedLicense` nas Ferramentas de linha de comando da Implementação de referência [!DNL Samples] diretório para código de amostra que demonstra licenças incorporadas.

>[!NOTE]
>
>Um cliente Adobe Primetime DRM 2.0 ignora todas as licenças incorporadas ao conteúdo e, em seguida, tenta obter uma licença do servidor de licenças especificado nos metadados. No entanto, se os metadados indicarem que nenhum servidor de licença está disponível, um cliente do Primetime DRM 2.0 precisará ser atualizado para que você possa visualizar o conteúdo.
