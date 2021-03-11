---
description: Para continuar emitindo licenças para o conteúdo que foi empacotado com o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, você deve migrar os dados da licença e da política de DRM do servidor LiveCycle ES para o novo servidor do cliente baseado no Adobe Primetime DRM SDK.
title: Migrar do FMRMS 1.0 ou 1.5 para o Adobe Primetime DRM 2.0 ou posterior
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Migrar do FMRMS 1.0 ou 1.5 para o Adobe Primetime DRM 2.0 ou posterior{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Para continuar emitindo licenças para o conteúdo que foi empacotado com o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, você deve migrar os dados da licença e da política de DRM do servidor LiveCycle ES para o novo servidor do cliente baseado no Adobe Primetime DRM SDK.

Para migrar, conclua as seguintes tarefas:

1. Informações da licença de importação:

   1. Para importar informações de licença do LiveCycle ES para o servidor baseado em DRM do Primetime, consulte os scripts de banco de dados de amostra na pasta [!DNL Reference Implementation\Server\migration\db].
   1. Execute os scripts de amostra para exportar dados relevantes de um banco de dados MySQL, Oracle ou SQL Server para um formato de arquivo CSV.
   1. Depois de exportar os dados do LiveCycle ES, importe os dados para o banco de dados.

      As informações da licença exportada incluem:

      * Uma ID de licença
      * Uma ID de conteúdo atribuída no momento do empacotamento
      * A ID da política de DRM que está sendo aplicada
      * O horário em que o conteúdo foi empacotado
      * A chave de criptografia de conteúdo

      Essas informações são necessárias antes de converter os metadados de conteúdo 1.x para o formato de metadados DRM do Primetime. Na implementação de referência, esses dados são armazenados na tabela de banco de dados de Licenças e são usados por `RefImplMetadataConvReqHandler`. Para obter mais informações, consulte `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`.


1. Converta as políticas FMRMS no formato DRM do Primetime:

   1. Antes de aplicar as políticas de DRM para converter metadados e emitir licenças para conteúdo da versão 1.0 ou 1.5, converta as políticas de DRM existentes para o formato de DRM do Primetime.

      A pasta `Reference Implementation\Server\migration` inclui um código de amostra para criar uma política de DRM do Primetime baseada em políticas de DRM mais antigas. Para migrar do FMRMS 1.0 para o Primetime DRM , consulte a amostra `V1_0PolicyConverter.java`.
   1. Compile o código de amostra executando o script `ant-f build-migration.xml build-1.0-converter`, que pesquisa as bibliotecas DRM 1.0 e Primetime nos diretórios [!DNL libs/1.0] e [!DNL libs/flashaccess].

   1. Edite o arquivo [!DNL converter.properties] para apontar para o servidor LiveCycle ES.
   1. Execute `ant -f build-migration.xml migrate-all-1.0-policies` para converter todas as políticas de DRM FMRMS 1.0 para o formato Primetime DRM.

      Para migrar do FMRMS 1.5 para o Primetime DRM , consulte a amostra `V1_5PolicyConverter.java`.

   1. Compile o código de amostra executando o script `ant-f build-migration.xml build-1.5-converter`, que espera que as bibliotecas 1.5 e 3.0 estejam nos diretórios [!DNL libs/1.5] e [!DNL libs/flashaccess].

   1. Edite o arquivo [!DNL converter.properties] para apontar para o servidor LiveCycle ES.
   1. Execute `ant -f build-migration.xml migrate-all-1.5-policies` para converter todas as políticas de DRM FMRMS 1.5 para o formato Primetime DRM.

      As políticas de DRM convertidas são salvas como um conjunto de arquivos. O `DRM PolicyConverter` gera um arquivo no formato CSV que inclui o mapeamento das IDs da política DRM antigas para as novas IDs da política DRM. Você pode importar esse arquivo para a tabela [!DNL PolicyConversion] no banco de dados de implementação de referência, onde ele é usado por `RefImplMetadataConvReqHandler`.

1. Suporta as solicitações de compatibilidade 1.x com as propriedades `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`:

   1. Depois que os dados relevantes forem migrados para um servidor baseado em DRM do Primetime, implemente o suporte para solicitações de compatibilidade 1.x.

      Para obter exemplos sobre como processar esses tipos de solicitações, consulte `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` na implementação de referência.

