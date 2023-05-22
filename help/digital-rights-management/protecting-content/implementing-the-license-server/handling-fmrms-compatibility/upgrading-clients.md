---
description: Há dois tipos de solicitações relacionados à compatibilidade do Flash Media Rights Management Server 1.x. Um tipo de solicitação é usado para solicitar que os clientes 1.x atualizem para um tempo de execução compatível com o Adobe Primetime DRM 2.0 ou posterior. Outra é usada para atualizar os metadados 1.x para o formato DRM do Primetime antes que uma licença possa ser solicitada. O suporte para essas solicitações só será necessário se você tiver implantado anteriormente qualquer conteúdo que use o FMRMS 1.0 ou 1.5.
title: Manuseio de compatibilidade de FMRMS
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# Manuseio de compatibilidade de FMRMS {#handling-fmrms-compatibility}

Há dois tipos de solicitações relacionados à compatibilidade do Flash Media Rights Management Server 1.x. Um tipo de solicitação é usado para solicitar que os clientes 1.x atualizem para um tempo de execução compatível com o Adobe Primetime DRM 2.0 ou posterior. Outra é usada para atualizar os metadados 1.x para o formato DRM do Primetime antes que uma licença possa ser solicitada. O suporte para essas solicitações só será necessário se você tiver implantado anteriormente qualquer conteúdo que use o FMRMS 1.0 ou 1.5.

## Atualização de clientes {#upgrading-clients}

Se um cliente FMRMS 1.x contatar um servidor DRM da Adobe Primetime, o servidor precisará solicitar que o cliente atualize.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* O URL da solicitação é &quot;*URL base do conteúdo 1.x*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   Ao contrário de outros manipuladores de solicitações do Adobe Primetime, esse manipulador não fornece acesso a nenhuma informação de solicitação ou requer que dados de resposta sejam definidos. Crie uma instância do `FMRMSv1RequestHandler`, e chame `close()`

## Atualização de metadados {#upgrading-metadata}

Se um cliente Adobe Primetime DRM encontrar conteúdo empacotado com o Flash Media Rights Management Server 1.x, ele extrairá os metadados de criptografia do conteúdo e os enviará para o servidor. Em seguida, o servidor converte os metadados do FMRMS 1.x no formato DRM do Primetime e os envia ao cliente. O cliente envia os metadados atualizados em uma solicitação de licença padrão do Primetime DRM.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* O URL da solicitação é &quot;*URL base do conteúdo 1.x*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

A conversão de metadados pode ser feita em tempo real quando o servidor recebe os metadados antigos do cliente. Como alternativa, o servidor poderia pré-processar o conteúdo antigo e armazenar os metadados convertidos; nesse caso, quando o cliente solicita novos metadados, o servidor precisa apenas buscar os novos metadados que correspondem ao identificador de licença dos metadados antigos.

Para converter metadados, o servidor deve executar as seguintes etapas:

* Obter `LiveCycleKeyMetaData`. Para pré-converter os metadados, `LiveCycleKeyMetaData` pode ser obtido de um arquivo empacotado 1.x usando `MediaEncrypter.examineEncryptedContent()`. Os metadados também são incluídos na solicitação de conversão de metadados ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Obtenha o identificador de licença dos metadados antigos e localize a chave de criptografia e as políticas DRM (essas informações estavam originalmente no banco de dados ES do Adobe LiveCycle). As políticas DRM ES do LiveCycle devem ser convertidas em políticas DRM do Primetime DRM 2.0.) A Implementação de referência inclui scripts e código de amostra para conversão das políticas de DRM e exportação de informações de licença do LiveCycle ES.
* Preencha o `V2KeyParameters` objeto (que você recupera chamando `MediaEncrypter.getKeyParameters()`).

* Carregue o `SigningCredential`, que é a credencial do empacotador emitida pelo Adobe usado para assinar metadados de criptografia. Obtenha o `SignatureParameters` ao chamar `MediaEncrypter.getSignatureParameters()` e preencha a credencial de assinatura.

* Chame `MetaDataConverter.convertMetadata()` para obter a `V2ContentMetaData`.

* Chame `V2ContentMetaData.getBytes()` e armazenar para uso futuro, ou chamar `FMRMSv1MetadataHandler.setUpdatedMetadata()`.