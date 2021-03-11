---
description: Há dois tipos de solicitações relacionadas à compatibilidade do Flash Media Rights Management Server 1.x. Um tipo de solicitação é usado para solicitar que clientes 1.x atualizem para um tempo de execução compatível com Adobe Primetime DRM 2.0 ou posterior. Outro é usado para atualizar os metadados 1.x para o formato DRM do Primetime antes que uma licença possa ser solicitada. O suporte para essas solicitações só é necessário se você implantou anteriormente qualquer conteúdo que use o FMRMS 1.0 ou 1.5.
title: Manipulação da compatibilidade com o FMRMS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# Lidando com a compatibilidade de FMRMS {#handling-fmrms-compatibility}

Há dois tipos de solicitações relacionadas à compatibilidade do Flash Media Rights Management Server 1.x. Um tipo de solicitação é usado para solicitar que clientes 1.x atualizem para um tempo de execução compatível com Adobe Primetime DRM 2.0 ou posterior. Outro é usado para atualizar os metadados 1.x para o formato DRM do Primetime antes que uma licença possa ser solicitada. O suporte para essas solicitações só é necessário se você implantou anteriormente qualquer conteúdo que use o FMRMS 1.0 ou 1.5.

## Atualizando clientes {#upgrading-clients}

Se um cliente FMRMS 1.x entrar em contato com um servidor DRM da Adobe Primetime, o servidor precisará solicitar que o cliente atualize.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* O URL da solicitação é &quot;*URL base do conteúdo 1.x*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   Ao contrário de outros manipuladores de solicitação do Adobe Primetime, esse manipulador não fornece acesso a informações de solicitação ou requer a definição de dados de resposta. Crie uma instância do `FMRMSv1RequestHandler` e chame `close()`

## Atualização de metadados {#upgrading-metadata}

Se um cliente DRM da Adobe Primetime encontrar conteúdo empacotado com o Flash Media Rights Management Server 1.x, ele extrai os metadados de criptografia do conteúdo e os envia ao servidor. Em seguida, o servidor converte os metadados FMRMS 1.x no formato DRM do Primetime e os envia para o cliente. Em seguida, o cliente envia os metadados atualizados em uma solicitação de licença padrão de DRM do Primetime.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* O URL da solicitação é &quot;*URL base do conteúdo 1.x*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

A conversão de metadados pode ser feita imediatamente quando o servidor recebe os metadados antigos do cliente. Como alternativa, o servidor poderia pré-processar o conteúdo antigo e armazenar os metadados convertidos; nesse caso, quando o cliente solicita novos metadados, o servidor precisa apenas buscar os novos metadados correspondentes ao identificador de licença dos metadados antigos.

Para converter metadados, o servidor deve executar as seguintes etapas:

* Obtenha `LiveCycleKeyMetaData`. Para pré-converter os metadados, `LiveCycleKeyMetaData` pode ser obtido de um arquivo empacotado 1.x usando `MediaEncrypter.examineEncryptedContent()`. Os metadados também são incluídos na solicitação de conversão de metadados ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Obtenha o identificador de licença dos metadados antigos e localize a chave de criptografia e as políticas de DRM (essas informações eram originalmente do banco de dados Adobe LiveCycle ES. As políticas de DRM LiveCycle ES devem ser convertidas em políticas de DRM Primetime 2.0.) A Implementação de referência inclui scripts e códigos de amostra para converter as políticas de DRM e exportar informações de licença do LiveCycle ES.
* Preencha o objeto `V2KeyParameters` (que você recupera chamando `MediaEncrypter.getKeyParameters()`).

* Carregue o `SigningCredential`, que é a credencial do empacotador emitida pelo Adobe para assinar metadados de criptografia. Obtenha o objeto `SignatureParameters` chamando `MediaEncrypter.getSignatureParameters()` e preencha a credencial de assinatura.

* Chame `MetaDataConverter.convertMetadata()` para obter o `V2ContentMetaData`.

* Chame `V2ContentMetaData.getBytes()` e armazene para uso futuro ou chame `FMRMSv1MetadataHandler.setUpdatedMetadata()`.