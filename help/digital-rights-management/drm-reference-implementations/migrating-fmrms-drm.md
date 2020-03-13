---
description: Para continuar emitindo licenças para conteúdo que foi empacotado com o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, você deve migrar dados de licença e política de DRM do servidor LiveCycle ES para o novo servidor do cliente que tem por base o SDK do Adobe Primetime DRM.
seo-description: Para continuar emitindo licenças para conteúdo que foi empacotado com o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, você deve migrar dados de licença e política de DRM do servidor LiveCycle ES para o novo servidor do cliente que tem por base o SDK do Adobe Primetime DRM.
seo-title: Migrar do FMRMS 1.0 ou 1.5 para o Adobe Primetime DRM 2.0 ou posterior
title: Migrar do FMRMS 1.0 ou 1.5 para o Adobe Primetime DRM 2.0 ou posterior
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Migrar do FMRMS 1.0 ou 1.5 para o Adobe Primetime DRM 2.0 ou posterior{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Para continuar emitindo licenças para conteúdo que foi empacotado com o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, você deve migrar dados de licença e política de DRM do servidor LiveCycle ES para o novo servidor do cliente que tem por base o SDK do Adobe Primetime DRM.

Para migrar, conclua as seguintes tarefas:

1. Importar informações da licença:

   1. Para importar informações de licença do LiveCycle ES para o servidor baseado em DRM do Primetime, consulte os scripts de banco de dados de amostra na [!DNL Reference Implementation\Server\migration\db] pasta.
   1. Execute os scripts de amostra para exportar dados relevantes de um banco de dados MySQL, Oracle ou SQL Server para um formato de arquivo CSV.
   1. Depois de exportar os dados do LiveCycle ES, importe os dados para o banco de dados.

      As informações da licença exportada incluem:

      * Uma ID de licença
      * Uma ID de conteúdo atribuída no momento do empacotamento
      * A ID da política de DRM que está sendo aplicada
      * A hora em que o conteúdo foi empacotado
      * A chave de criptografia do conteúdo
      Essas informações são necessárias para que você possa converter os metadados de conteúdo 1.x para o formato de metadados DRM do Primetime. Na implementação de referência, esses dados são armazenados na tabela do banco de dados de Licenças e são usados por `RefImplMetadataConvReqHandler`. For more information, see `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`.


1. Converta as políticas FMRMS no formato DRM do Primetime:

   1. Antes de aplicar as políticas de DRM para converter metadados e emitir licenças para conteúdo da versão 1.0 ou 1.5, converta as políticas de DRM existentes no formato DRM do Primetime.

      A `Reference Implementation\Server\migration` pasta inclui um código de amostra para criar uma política de DRM Primetime baseada em políticas de DRM mais antigas. Para migrar do FMRMS 1.0 para o Primetime DRM, consulte a `V1_0PolicyConverter.java` amostra.
   1. Compile o código de amostra executando `ant-f build-migration.xml build-1.0-converter` script, que pesquisa as bibliotecas 1.0 e Primetime DRM nos diretórios [!DNL libs/1.0] e [!DNL libs/flashaccess] .

   1. Edite o [!DNL converter.properties] arquivo para apontar para o servidor do LiveCycle ES.
   1. Execute `ant -f build-migration.xml migrate-all-1.0-policies` para converter todas as políticas de DRM do FMRMS 1.0 para o formato DRM do Primetime.

      Para migrar do FMRMS 1.5 para o Primetime DRM, consulte a `V1_5PolicyConverter.java` amostra.

   1. Compile o código de amostra executando o `ant-f build-migration.xml build-1.5-converter` script, que espera que as bibliotecas 1.5 e 3.0 estejam nos diretórios [!DNL libs/1.5] e [!DNL libs/flashaccess] .

   1. Edite o [!DNL converter.properties] arquivo para apontar para o servidor do LiveCycle ES.
   1. Execute `ant -f build-migration.xml migrate-all-1.5-policies` para converter todas as políticas de DRM do FMRMS 1.5 para o formato DRM do Primetime.

      As políticas de DRM convertidas são salvas como um conjunto de arquivos. O `DRM PolicyConverter` gera um arquivo formatado em CSV que inclui o mapeamento das IDs de política DRM antigas para as novas IDs de política DRM. É possível importar esse arquivo para a [!DNL PolicyConversion] tabela no banco de dados de implementação de referência, onde ele é usado por `RefImplMetadataConvReqHandler`.

1. Suporta as solicitações de compatibilidade 1.x com as propriedades `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler` :

   1. Depois que os dados relevantes forem migrados para um servidor baseado em DRM Primetime, implemente suporte para solicitações de compatibilidade 1.x.

      Para obter exemplos sobre como processar esses tipos de solicitações, consulte `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` na implementação de referência.

