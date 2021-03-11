---
description: Essas classes fornecem metadados para anúncios, namespaces e rastreamento.
title: Classes de metadados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Classes de metadados{#metadata-classes}

Essas classes fornecem metadados para anúncios, namespaces e rastreamento.

Pacote: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nome | Descrição |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Classe que fornece propriedades que devem ser configuradas para a resolução de anúncios para um determinado item de mídia. Todas as propriedades necessárias devem ser definidas para configurar o reprodutor para resolver anúncios com êxito. |
| AuditudeMetadata | Obsoleto. Use AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe que estende o Java `AdvertisingMetadata` especificamente para Frase. Fornece propriedades a serem configuradas para resolver Anúncios de frases para um determinado item de mídia. Você deve definir todas as propriedades necessárias, incluindo ID de zona, ID de mídia e URL do servidor de publicidade, para configurar o reprodutor para resolver anúncios com êxito. |
| [Metadados](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Define a interface genérica para configurar todos os metadados disponíveis para o player e objetos adicionais. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Classe genérica com estrutura de dados para armazenar pares de valores-chave arbitrários. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe para a representação bruta dos metadados cronometrados inseridos em um fluxo de mídia. |