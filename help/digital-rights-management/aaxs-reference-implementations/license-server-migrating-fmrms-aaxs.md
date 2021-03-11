---
title: Migração do FMRMS 1.0 ou 1.5 para o Adobe Access 2.0 e superior
description: Migração do FMRMS 1.0 ou 1.5 para o Adobe Access 2.0 e superior
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Migração do FMRMS 1.0 ou 1.5 para o Adobe Access 2.0 e superior {#migrating-from-fmrms-or-to-adobe-access-and-above}

Para continuar a emitir licenças para o conteúdo empacotado usando o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, os dados de licença e política devem ser migrados do servidor LiveCycle ES para o novo servidor do cliente com base no SDK de Acesso do Adobe. As etapas importantes são:

1. Importando informações de licença
1. Conversão das políticas FMRMS para o formato Adobe Access
1. Suporte às solicitações de compatibilidade 1.x por meio de `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`

Para importar informações de licença do LiveCycle ES para o servidor baseado no Adobe Access, consulte os scripts de banco de dados de amostra fornecidos na pasta [!DNL Reference Implementation\Server\migration\db]. São fornecidos scripts de amostra para exportar os dados relevantes de um banco de dados MySQL, Oracle ou SQL Server para um formato de arquivo CSV. Após os dados serem exportados, eles poderão ser importados para o banco de dados de sua escolha. As informações da licença exportada incluem a ID da licença, uma ID de conteúdo atribuída no momento do empacotamento, a ID da política usada, o momento em que o conteúdo foi empacotado e a chave de criptografia de conteúdo. Para o Acesso ao Adobe, essas informações são necessárias para converter os metadados de conteúdo 1.x no formato de metadados do Acesso ao Adobe (consulte `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`). Na implementação de referência, esses dados são armazenados na tabela de banco de dados de Licenças e usados por `RefImplMetadataConvReqHandler`.

As políticas existentes precisarão ser convertidas no formato de Adobe Access para usar essas políticas ao converter metadados e emitir licenças para conteúdo 1.0 ou 1.5. Referência Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies.

Se estiver migrando do FMRMS 1.0 para o Adobe Access, consulte a amostra V1_0PolicyConverter.java . Compile o código de amostra executando &quot; `ant-f build-migration.xml build-1.0-converter`&quot; (o script espera que as bibliotecas 1.0 e Adobe Access estejam em [!DNL libs/1.0] e libs/flashaccess, respectivamente). Edite o arquivo conversor.properties para apontar para o servidor ES do LiveCycle. Em seguida, execute &quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot; para converter todas as políticas FMRMS 1.0 para o formato Adobe Access .

Se estiver migrando do FMRMS 1.5 para o Adobe Access, consulte a amostra V1_5PolicyConverter.java . Compile o código de amostra executando &quot; `ant-f build-migration.xml build-1.5-converter`&quot; (o script espera que as bibliotecas 1.5 e 3.0 estejam em libs/1.5 e libs/flashaccess respectivamente). Edite o arquivo conversor.properties para apontar para o servidor ES do LiveCycle. Em seguida, execute &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; para converter todas as políticas FMRMS 1.5 para o formato Adobe Access .

As políticas convertidas serão gravadas em um conjunto de arquivos. Além disso, o PolicyConverter gerará um arquivo CSV contendo o mapeamento de IDs de política antigas para novas IDs de política. Esse arquivo pode ser importado para a tabela &quot;PolicyConversion&quot; no banco de dados de implementação de referência e será usado por `RefImplMetadataConvReqHandler`.

Depois que os dados relevantes forem migrados para o servidor baseado no Adobe Access, você estará pronto para implementar o suporte para solicitações de compatibilidade 1.x. Consulte `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` na implementação de referência para obter exemplos de como processar esses tipos de solicitações.
