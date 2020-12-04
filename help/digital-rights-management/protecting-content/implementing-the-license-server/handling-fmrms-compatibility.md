---
description: Tratamento da compatibilidade FMRMS
seo-description: Tratamento da compatibilidade FMRMS
seo-title: Atualizando clientes
title: Atualizando clientes
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Tratamento da compatibilidade FMRMS {#handling-fmrms-compatibility}

Há dois tipos de solicitações relacionadas à compatibilidade do Flash Media Rights Management Server 1.x. Um tipo de solicitação é usado para solicitar que os clientes 1.x atualizem para um tempo de execução compatível com o Adobe Primetime DRM 2.0 ou posterior. Outro é usado para atualizar os metadados 1.x para o formato DRM Primetime antes que uma licença possa ser solicitada. O suporte para essas solicitações só é necessário se você implantou previamente qualquer conteúdo que use o FMRMS 1.0 ou 1.5.

## Atualizando clientes {#upgrading-clients}

Se um cliente FMRMS 1.x entrar em contato com um servidor DRM da Adobe Primetime, o servidor precisará solicitar que o cliente atualize.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* O URL da solicitação é &quot;*URL base de conteúdo 1.x*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   Ao contrário de outros manipuladores de solicitação da Adobe Primetime, esse manipulador não fornece acesso a nenhuma informação de solicitação ou exige que qualquer dado de resposta seja definido. Crie uma instância de `FMRMSv1RequestHandler` e chame `close()`

## Atualização de metadados {#upgrading-metadata}

Se um cliente do Adobe Access encontrar conteúdo empacotado com o Flash Media Rights Management Server 1.x, ele extrairá os metadados de criptografia do conteúdo e os enviará para o servidor. O servidor converterá os metadados FMRMS 1.x no formato de Acesso ao Adobe e os enviará de volta ao cliente. Em seguida, o cliente envia os metadados atualizados em uma solicitação de licença padrão de acesso a Adobe.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* O URL da solicitação é &quot;*URL base de conteúdo 1.x*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

A conversão de metadados pode ser feita dinamicamente quando o servidor recebe os metadados antigos do cliente. Como alternativa, o servidor poderia pré-processar o conteúdo antigo e armazenar os metadados convertidos; nesse caso, quando o cliente solicita novos metadados, o servidor precisa apenas buscar os novos metadados correspondentes ao identificador de licença dos metadados antigos.

Para converter metadados, o servidor deve executar as seguintes etapas:

* Obtenha `LiveCycleKeyMetaData`. Para pré-converter os metadados, `LiveCycleKeyMetaData` pode ser obtido de um arquivo compactado 1.x usando `MediaEncrypter.examineEncryptedContent()`. Os metadados também são incluídos na solicitação de conversão de metadados ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Obtenha o identificador de licença dos metadados antigos e localize a chave de criptografia e as políticas (essas informações estavam originalmente no banco de dados ES do LiveCycle Adobe. As políticas do LiveCycle ES devem ser convertidas em políticas do Adobe Access 2.0.) A Implementação de referência inclui scripts e códigos de amostra para converter as políticas e exportar informações de licença do LiveCycle ES.
* Preencha o objeto `V2KeyParameters` (que você recupera chamando `MediaEncrypter.getKeyParameters()`).
* Carregue `SigningCredential`, que é a credencial do Packager emitida pelo Adobe usado para assinar metadados de criptografia. Obtenha o objeto `SignatureParameters` chamando `MediaEncrypter.getSignatureParameters()` e preencha a credencial de assinatura.
* Chame `MetaDataConverter.convertMetadata()` para obter o `V2ContentMetaData`.
* Chame `V2ContentMetaData.getBytes()` e armazene para uso futuro, ou chame `FMRMSv1MetadataHandler.setUpdatedMetadata()`.