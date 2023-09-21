---
description: Essas classes fornecem metadados para publicidade, namespaces e rastreamento.
title: Classes de metadados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Classes de metadados{#metadata-classes}

Essas classes fornecem metadados para publicidade, namespaces e rastreamento.

Pacote: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nome | Descrição |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Classe que fornece propriedades que devem ser configuradas para resolver anúncios para um determinado item de mídia. Todas as propriedades necessárias devem ser definidas para configurar o reprodutor para resolver anúncios com sucesso. |
| AuditudeMetadata | Obsoleto. Use o AuditudeSettings. |
| [ConfiguraçõesAuditoria](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe que estende o Java `AdvertisingMetadata` especificamente para a Frase. Fornece propriedades a serem configuradas para resolver anúncios de frases para um determinado item de mídia. Você deve definir todas as propriedades necessárias, incluindo ID de zona, ID de mídia e URL do servidor de anúncios, para configurar o reprodutor para resolver anúncios com sucesso. |
| [Metadados](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Define a interface genérica para configurar todos os metadados disponíveis para o player e objetos adicionais. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Classe genérica semelhante à estrutura de dados para armazenar pares arbitrários de valores-chave. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe para a representação bruta dos metadados cronometrados inseridos em um fluxo de mídia. |
