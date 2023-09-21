---
description: Para continuar a emitir licenças para conteúdo que foi empacotado com o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, você deve migrar os dados de licença e política DRM do servidor ES do LiveCycle para o novo servidor do cliente baseado no SDK do Adobe Primetime DRM.
title: Migração do FMRMS 1.0 ou 1.5 para o Adobe Primetime DRM 2.0 ou posterior
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Migração do FMRMS 1.0 ou 1.5 para o Adobe Primetime DRM 2.0 ou posterior{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

Para continuar a emitir licenças para conteúdo que foi empacotado com o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, você deve migrar os dados de licença e política DRM do servidor ES do LiveCycle para o novo servidor do cliente baseado no SDK do Adobe Primetime DRM.

Para migrar, conclua as seguintes tarefas:

1. Informações de licença de importação:

   1. Para importar informações de licença do LiveCycle ES para o servidor baseado no Primetime DRM, consulte os exemplos de scripts de banco de dados no [!DNL Reference Implementation\Server\migration\db] pasta.
   1. Execute os scripts de amostra para exportar dados relevantes de um banco de dados MySQL, Oracle ou SQL Server para um formato de arquivo CSV.
   1. Após exportar os dados do LiveCycle ES, importe-os para o banco de dados.

      As informações de licença exportadas incluem o seguinte:

      * Uma ID de licença
      * Uma ID de conteúdo atribuída no momento do empacotamento
      * A ID da política DRM que está sendo aplicada
      * A hora em que o conteúdo foi empacotado
      * A chave de criptografia do conteúdo

      Essas informações são necessárias antes de converter os metadados de conteúdo 1.x para o formato de metadados DRM do Primetime. Na implementação de referência, esses dados são armazenados na tabela do banco de dados Licença e são usados por `RefImplMetadataConvReqHandler`. Para obter mais informações, consulte `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`.

1. Converter políticas de FMRMS no formato DRM Primetime:

   1. Antes de aplicar as políticas DRM para converter metadados e emitir licenças para conteúdo da versão 1.0 ou 1.5, converta as políticas DRM existentes para o formato DRM do Primetime.

      A variável `Reference Implementation\Server\migration` A pasta inclui código de amostra para criar uma política de DRM do Primetime baseada em políticas de DRM mais antigas. Para migrar do FMRMS 1.0 para o Primetime DRM, consulte o `V1_0PolicyConverter.java` amostra.
   1. Compilar o código de amostra executando `ant-f build-migration.xml build-1.0-converter` que pesquisa as bibliotecas DRM 1.0 e Primetime no [!DNL libs/1.0] e [!DNL libs/flashaccess] diretórios.

   1. Edite o [!DNL converter.properties] para apontar para o servidor LiveCycle ES.
   1. Executar `ant -f build-migration.xml migrate-all-1.0-policies` para converter todas as políticas DRM do FMRMS 1.0 para o formato DRM Primetime.

      Para migrar do FMRMS 1.5 para o Primetime DRM, consulte o `V1_5PolicyConverter.java` amostra.

   1. Compilar o código de amostra executando `ant-f build-migration.xml build-1.5-converter` que espera que as bibliotecas 1.5 e 3.0 estejam no estado [!DNL libs/1.5] e [!DNL libs/flashaccess] diretórios.

   1. Edite o [!DNL converter.properties] para apontar para o servidor LiveCycle ES.
   1. Executar `ant -f build-migration.xml migrate-all-1.5-policies` para converter todas as políticas DRM do FMRMS 1.5 para o formato DRM Primetime.

      As políticas DRM convertidas são salvas como um conjunto de arquivos. A variável `DRM PolicyConverter` O gera um arquivo formatado em CSV que inclui o mapeamento das IDs de política DRM antigas para as novas IDs de política DRM. Você pode importar esse arquivo para o [!DNL PolicyConversion] tabela na base de dados de implementação de referência, onde é usada pelo `RefImplMetadataConvReqHandler`.

1. Suporte às solicitações de compatibilidade 1.x com o `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler` propriedades:

   1. Depois que os dados relevantes forem migrados para um servidor baseado em DRM do Primetime, implemente o suporte para solicitações de compatibilidade 1.x.

      Para obter exemplos sobre como processar esses tipos de solicitações, consulte `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` na implementação de referência.
