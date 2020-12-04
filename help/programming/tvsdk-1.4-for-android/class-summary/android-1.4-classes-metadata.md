---
description: Essas classes fornecem metadados para publicidade, namespaces e rastreamento.
seo-description: Essas classes fornecem metadados para publicidade, namespaces e rastreamento.
seo-title: Classes de metadados
title: Classes de metadados
uuid: 6d5099c8-d562-4635-9ef0-068cc6fb9f82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Classes de metadados{#metadata-classes}

Essas classes fornecem metadados para publicidade, namespaces e rastreamento.

Pacote: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nome | Descrição |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Classe que fornece propriedades que devem ser configuradas para resolver anúncios para um determinado item de mídia. Todas as propriedades necessárias devem ser definidas para configurar o player para a resolução bem-sucedida de anúncios. |
| AuditudeMetadata | Obsoleto. Use AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe que estende Java `AdvertisingMetadata` especificamente para Frase. Fornece propriedades a serem configuradas para resolver anúncios de frases para um determinado item de mídia. Você deve definir todas as propriedades necessárias, incluindo a ID da zona, a ID da mídia e o URL do servidor de publicidade, para configurar o player para resolver anúncios com êxito. |
| [Metadados](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Define a interface genérica para configurar todos os metadados disponíveis para o player e objetos adicionais. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Classe genérica semelhante à estrutura de dados para armazenar pares de valores chave arbitrários. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe para a representação bruta dos metadados cronometrados inseridos em um fluxo de mídia. |