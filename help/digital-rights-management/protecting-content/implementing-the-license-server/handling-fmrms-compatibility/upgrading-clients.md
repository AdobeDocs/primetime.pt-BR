---
description: Há dois tipos de solicitações relacionadas à compatibilidade do Flash Media Rights Management Server 1.x. Um tipo de solicitação é usado para solicitar que os clientes 1.x atualizem para um tempo de execução compatível com o Adobe Primetime DRM 2.0 ou posterior. Outro é usado para atualizar os metadados 1.x para o formato DRM Primetime antes que uma licença possa ser solicitada. O suporte para essas solicitações só é necessário se você implantou previamente qualquer conteúdo que use o FMRMS 1.0 ou 1.5.
seo-description: Há dois tipos de solicitações relacionadas à compatibilidade do Flash Media Rights Management Server 1.x. Um tipo de solicitação é usado para solicitar que os clientes 1.x atualizem para um tempo de execução compatível com o Adobe Primetime DRM 2.0 ou posterior. Outro é usado para atualizar os metadados 1.x para o formato DRM Primetime antes que uma licença possa ser solicitada. O suporte para essas solicitações só é necessário se você implantou previamente qualquer conteúdo que use o FMRMS 1.0 ou 1.5.
seo-title: Tratamento da compatibilidade FMRMS
title: Tratamento da compatibilidade FMRMS
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Tratamento da compatibilidade FMRMS {#handling-fmrms-compatibility}

Há dois tipos de solicitações relacionadas à compatibilidade do Flash Media Rights Management Server 1.x. Um tipo de solicitação é usado para solicitar que os clientes 1.x atualizem para um tempo de execução compatível com o Adobe Primetime DRM 2.0 ou posterior. Outro é usado para atualizar os metadados 1.x para o formato DRM Primetime antes que uma licença possa ser solicitada. O suporte para essas solicitações só é necessário se você implantou previamente qualquer conteúdo que use o FMRMS 1.0 ou 1.5.

## Atualizando clientes {#upgrading-clients}

Se um cliente FMRMS 1.x entrar em contato com um servidor DRM do Adobe Primetime, o servidor precisará solicitar a atualização do cliente.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* O URL da solicitação é &quot;URL *base de conteúdo* 1.x&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   Ao contrário de outros manipuladores de solicitação do Adobe Primetime, esse manipulador não fornece acesso a nenhuma informação de solicitação ou requer que qualquer dado de resposta seja definido. Crie uma instância do `FMRMSv1RequestHandler`, em seguida, chame `close()`

## Atualização de metadados {#upgrading-metadata}

Se um cliente Adobe Primetime DRM encontrar conteúdo empacotado com o Flash Media Rights Management Server 1.x, ele extrai os metadados de criptografia do conteúdo e os envia para o servidor. Em seguida, o servidor converte os metadados FMRMS 1.x no formato DRM do Primetime e os envia para o cliente. O cliente envia os metadados atualizados em uma solicitação de licença padrão do Primetime DRM.

* A classe do manipulador de solicitação é `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* O URL da solicitação é &quot;URL *base de conteúdo* 1.x&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

A conversão de metadados pode ser feita dinamicamente quando o servidor recebe os metadados antigos do cliente. Como alternativa, o servidor poderia pré-processar o conteúdo antigo e armazenar os metadados convertidos; nesse caso, quando o cliente solicita novos metadados, o servidor precisa apenas buscar os novos metadados correspondentes ao identificador de licença dos metadados antigos.

Para converter metadados, o servidor deve executar as seguintes etapas:

* Vá `LiveCycleKeyMetaData`. Para pré-converter os metadados, `LiveCycleKeyMetaData` é possível obter de um arquivo empacotado 1.x usando `MediaEncrypter.examineEncryptedContent()`. Os metadados também são incluídos na solicitação de conversão de metadados ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Obtenha o identificador de licença dos metadados antigos e localize a chave de criptografia e as políticas de DRM (essas informações estavam originalmente no banco de dados do Adobe LiveCycle ES. As políticas do LiveCycle ES DRM devem ser convertidas em políticas do Primetime DRM 2.0.) A Implementação de referência inclui scripts e códigos de amostra para converter as políticas de DRM e exportar informações de licença do LiveCycle ES.
* Preencha o `V2KeyParameters` objeto (que você recupera chamando `MediaEncrypter.getKeyParameters()`).

* Carregue o `SigningCredential`, que é a credencial do Packager emitida pela Adobe usada para assinar metadados de criptografia. Obtenha o `SignatureParameters` objeto chamando `MediaEncrypter.getSignatureParameters()` e preenchendo a credencial de assinatura.

* Ligue `MetaDataConverter.convertMetadata()` para obter o `V2ContentMetaData`.

* Chame `V2ContentMetaData.getBytes()` e armazene para uso futuro, ou chame `FMRMSv1MetadataHandler.setUpdatedMetadata()`.