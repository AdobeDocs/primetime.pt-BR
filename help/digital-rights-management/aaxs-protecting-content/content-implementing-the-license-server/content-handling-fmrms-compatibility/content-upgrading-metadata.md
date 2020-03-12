---
seo-title: Atualização de metadados
title: Atualização de metadados
uuid: cad0b23e-50ca-47ae-871f-be571cb00a26
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Atualização de metadados{#upgrading-metadata}

Se um cliente do Adobe Access encontrar conteúdo empacotado com o Flash Media Rights Management Server 1.x, ele extrairá os metadados de criptografia do conteúdo e os enviará para o servidor. O servidor converterá os metadados FMRMS 1.x no formato Adobe Access e os enviará de volta ao cliente. O cliente envia os metadados atualizados em uma solicitação de licença padrão do Adobe Access.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* O URL da solicitação é &quot;URL *base de conteúdo* 1.x&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

A conversão de metadados pode ser feita dinamicamente quando o servidor recebe os metadados antigos do cliente. Como alternativa, o servidor poderia pré-processar o conteúdo antigo e armazenar os metadados convertidos; nesse caso, quando o cliente solicita novos metadados, o servidor precisa apenas buscar os novos metadados correspondentes ao identificador de licença dos metadados antigos.

Para converter metadados, o servidor deve executar as seguintes etapas:

* Vá `LiveCycleKeyMetaData`. Para pré-converter os metadados, `LiveCycleKeyMetaData` é possível obter de um arquivo empacotado 1.x usando `MediaEncrypter.examineEncryptedContent()`. Os metadados também são incluídos na solicitação de conversão de metadados ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Obtenha o identificador de licença dos metadados antigos e localize a chave de criptografia e as políticas (essas informações foram originalmente encontradas no banco de dados do Adobe LiveCycle ES. As políticas do LiveCycle ES devem ser convertidas em políticas do Adobe Access 2.0.) A Implementação de referência inclui scripts e códigos de amostra para converter as políticas e exportar informações de licença do LiveCycle ES.
* Preencha o `V2KeyParameters` objeto (que você recupera chamando `MediaEncrypter.getKeyParameters()`).
* Carregue o `SigningCredential`, que é a credencial do Packager emitida pela Adobe usada para assinar metadados de criptografia. Obtenha o `SignatureParameters` objeto chamando `MediaEncrypter.getSignatureParameters()` e preenchendo a credencial de assinatura.
* Ligue `MetaDataConverter.convertMetadata()` para obter o `V2ContentMetaData`.
* Chame `V2ContentMetaData.getBytes()` e armazene para uso futuro, ou chame `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

