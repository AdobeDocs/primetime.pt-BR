---
title: Atualização de metadados
description: Atualização de metadados
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Atualização de metadados{#upgrading-metadata}

Se um cliente de acesso ao Adobe encontrar conteúdo empacotado com o Flash Media Rights Management Server 1.x, ele extrairá os metadados de criptografia do conteúdo e os enviará ao servidor. O servidor converterá os metadados do FMRMS 1.x no formato de Acesso ao Adobe e os enviará de volta ao cliente. Em seguida, o cliente envia os metadados atualizados em uma solicitação padrão de licença de acesso ao Adobe.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* O URL da solicitação é &quot;*URL base do conteúdo 1.x*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

A conversão de metadados pode ser feita em tempo real quando o servidor recebe os metadados antigos do cliente. Como alternativa, o servidor poderia pré-processar o conteúdo antigo e armazenar os metadados convertidos; nesse caso, quando o cliente solicita novos metadados, o servidor precisa apenas buscar os novos metadados que correspondem ao identificador de licença dos metadados antigos.

Para converter metadados, o servidor deve executar as seguintes etapas:

* Obter `LiveCycleKeyMetaData`. Para pré-converter os metadados, `LiveCycleKeyMetaData` pode ser obtido de um arquivo empacotado 1.x usando `MediaEncrypter.examineEncryptedContent()`. Os metadados também são incluídos na solicitação de conversão de metadados ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Obtenha o identificador de licença dos metadados antigos e localize a chave de criptografia e as políticas (essas informações estavam originalmente no banco de dados ES do Adobe LiveCycle. As políticas do LiveCycle ES devem ser convertidas em políticas do Adobe Access 2.0.) A Implementação de referência inclui scripts e código de amostra para converter as políticas e exportar informações de licença do LiveCycle ES.
* Preencha o `V2KeyParameters` objeto (que você recupera chamando `MediaEncrypter.getKeyParameters()`).
* Carregue o `SigningCredential`, que é a credencial do empacotador emitida pelo Adobe usado para assinar metadados de criptografia. Obtenha o `SignatureParameters` ao chamar `MediaEncrypter.getSignatureParameters()` e preencha a credencial de assinatura.
* Chame `MetaDataConverter.convertMetadata()` para obter a `V2ContentMetaData`.
* Chame `V2ContentMetaData.getBytes()` e armazenar para uso futuro, ou chamar `FMRMSv1MetadataHandler.setUpdatedMetadata()`.
