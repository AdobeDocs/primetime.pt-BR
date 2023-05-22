---
description: Essas classes fornecem metadados para publicidade, namespaces e rastreamento.
title: Classes de metadados
exl-id: 4014b496-7fc4-4fa9-98da-28350668d35f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Classes de metadados {#metadata-classes}

Essas classes fornecem metadados para publicidade, namespaces e rastreamento.

Pacote: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/package-detail.html)

| Nome | Descrição |
|---|---|
| [ModoDeSinalizaçãoAnúncio](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AdSignalingMode.html) | Classe de enumeração que expõe os modos de sinalização compatíveis na Frase. |
| [ConfiguraçõesAuditoria](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe que estende `Metadata` especificamente para a Frase. Fornece propriedades a serem configuradas para resolver anúncios de frases para um determinado item de mídia. Você deve definir todas as propriedades necessárias, incluindo ID de zona, ID de mídia e URL do servidor de anúncios, para configurar o reprodutor para resolver anúncios com sucesso. |
| [ByteArrayMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/ByteArrayMetadata.html) | Obsoleto. Uso `Metadata`. |
| [DefaultMetadataKeys](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/DefaultMetadataKeys.html) | Classe. |
| [Metadados](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/Metadata.html) | Define a interface genérica para configurar todos os metadados disponíveis para o player e objetos adicionais. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Obsoleto. Uso `Metadata`. |
| [MetadataUtils](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataUtils.html) | Classe de métodos para trabalhar com metadados. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe para a representação bruta dos metadados cronometrados inseridos em um fluxo de mídia. |
| [TimedMetadataType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadataType.html) | Classe que contém os tipos suportados para metadados cronometrados (na lista de reprodução ou fluxo), como metadados ou tags de ID3. |
