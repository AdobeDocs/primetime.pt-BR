---
seo-title: Migração do FMRMS 1.0 ou 1.5 para o Adobe Access 2.0 e superior
title: Migração do FMRMS 1.0 ou 1.5 para o Adobe Access 2.0 e superior
uuid: 05caeb39-0c62-4053-87a9-8e89030a188d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Migração do FMRMS 1.0 ou 1.5 para o Adobe Access 2.0 e superior a {#migrating-from-fmrms-or-to-adobe-access-and-above}

Para continuar a emitir licenças para conteúdo empacotado usando o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, os dados de licença e política devem ser migrados do servidor ES do LiveCycle para o novo servidor do cliente com base no SDK de acesso do Adobe. As etapas importantes são:

1. Importando informações de licença
1. Converter políticas FMRMS em formato de Adobe Access
1. Suporte às solicitações de compatibilidade 1.x por meio de `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`

Para importar informações de licença do LiveCycle ES para o servidor baseado no Adobe Access, consulte as amostras de scripts de banco de dados fornecidas na pasta [!DNL Reference Implementation\Server\migration\db]. Scripts de amostra são fornecidos para exportar os dados relevantes de um banco de dados MySQL, Oracle ou SQL Server para um formato de arquivo CSV. Após os dados serem exportados, eles poderão ser importados para o banco de dados de sua escolha. As informações de licença exportadas incluem a ID de licença, uma ID de conteúdo atribuída no momento do empacotamento, a ID da política usada, o momento em que o conteúdo foi empacotado e a chave de criptografia do conteúdo. Para o Acesso ao Adobe, essas informações são necessárias para converter os metadados de conteúdo 1.x no formato de metadados do Acesso ao Adobe (consulte `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`). Na implementação de referência, esses dados são armazenados na tabela do banco de dados de Licenças e usados por `RefImplMetadataConvReqHandler`.

As políticas existentes precisarão ser convertidas no formato de Adobe Access para que essas políticas possam ser usadas ao converter metadados e emitir licenças para conteúdo 1.0 ou 1.5. A Referência Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies.

Se você estiver migrando do FMRMS 1.0 para o Adobe Access, consulte a amostra V1_0PolicyConverter.java. Compile o código de amostra executando &quot; `ant-f build-migration.xml build-1.0-converter`&quot; (o script espera que as bibliotecas 1.0 e Adobe Access estejam em [!DNL libs/1.0] e libs/flashaccess, respectivamente). Edite o arquivo converter.properties para apontar para o servidor ES do seu LiveCycle. Em seguida, execute &quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot; para converter todas as políticas do FMRMS 1.0 para o formato de acesso ao Adobe.

Se você estiver migrando do FMRMS 1.5 para o Adobe Access, consulte a amostra V1_5PolicyConverter.java. Compile o código de amostra executando &quot; `ant-f build-migration.xml build-1.5-converter`&quot; (o script espera que as bibliotecas 1.5 e 3.0 estejam em libs/1.5 e libs/flashaccess respectivamente). Edite o arquivo converter.properties para apontar para o servidor ES do seu LiveCycle. Em seguida, execute &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; para converter todas as políticas do FMRMS 1.5 para o formato de acesso ao Adobe.

As políticas convertidas serão gravadas em um conjunto de arquivos. Além disso, o PolicyConverter produzirá um arquivo CSV contendo o mapeamento de IDs de política antigas para novas IDs de política. Esse arquivo pode ser importado para a tabela &quot;PolicyConversion&quot; no banco de dados de implementação de referência e será usado por `RefImplMetadataConvReqHandler`.

Depois que os dados relevantes forem migrados para o servidor baseado no Adobe Access, você estará pronto para implementar o suporte para solicitações de compatibilidade 1.x. Consulte `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` na implementação de referência para obter exemplos de como processar esses tipos de solicitações.
