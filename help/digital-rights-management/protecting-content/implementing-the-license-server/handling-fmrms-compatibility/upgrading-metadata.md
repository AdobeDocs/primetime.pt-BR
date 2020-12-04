---
seo-title: Atualização de metadados
title: Atualização de metadados
uuid: 769483e6-a2d1-46cb-afcf-557aa807037c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Atualização de metadados{#upgrading-metadata}

Se um cliente Adobe Primetime DRM encontrar conteúdo empacotado com o Flash Media Rights Management Server 1.x, ele extrai os metadados de criptografia do conteúdo e os envia para o servidor. Em seguida, o servidor converte os metadados FMRMS 1.x no formato DRM do Primetime e os envia para o cliente. O cliente envia os metadados atualizados em uma solicitação de licença padrão do Primetime DRM.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* O URL da solicitação é &quot;*URL base de conteúdo 1.x*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

A conversão de metadados pode ser feita dinamicamente quando o servidor recebe os metadados antigos do cliente. Como alternativa, o servidor poderia pré-processar o conteúdo antigo e armazenar os metadados convertidos; nesse caso, quando o cliente solicita novos metadados, o servidor precisa apenas buscar os novos metadados correspondentes ao identificador de licença dos metadados antigos.

Para converter metadados, o servidor deve executar as seguintes etapas:

* Obtenha `LiveCycleKeyMetaData`. Para pré-converter os metadados, `LiveCycleKeyMetaData` pode ser obtido de um arquivo compactado 1.x usando `MediaEncrypter.examineEncryptedContent()`. Os metadados também são incluídos na solicitação de conversão de metadados ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Obtenha o identificador de licença dos metadados antigos e localize a chave de criptografia e as políticas de DRM (essas informações estavam originalmente no banco de dados ES do LiveCycle Adobe. As políticas de DRM do LiveCycle ES devem ser convertidas em políticas de DRM do Primetime DRM 2.0.) A Implementação de referência inclui scripts e exemplos de código para converter as políticas de DRM e exportar informações de licença do LiveCycle ES.
* Preencha o objeto `V2KeyParameters` (que você recupera chamando `MediaEncrypter.getKeyParameters()`).

* Carregue `SigningCredential`, que é a credencial do Packager emitida pelo Adobe usado para assinar metadados de criptografia. Obtenha o objeto `SignatureParameters` chamando `MediaEncrypter.getSignatureParameters()` e preencha a credencial de assinatura.

* Chame `MetaDataConverter.convertMetadata()` para obter o `V2ContentMetaData`.

* Chame `V2ContentMetaData.getBytes()` e armazene para uso futuro, ou chame `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

