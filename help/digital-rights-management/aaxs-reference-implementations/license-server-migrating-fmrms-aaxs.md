---
title: Migração de FMRMS 1.0 ou 1.5 para Adobe Access 2.0 e superior
description: Migração de FMRMS 1.0 ou 1.5 para Adobe Access 2.0 e superior
copied-description: true
exl-id: 9aadf9a0-a7c5-466b-9dd1-c1bab2b8bfc6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Migração de FMRMS 1.0 ou 1.5 para Adobe Access 2.0 e superior {#migrating-from-fmrms-or-to-adobe-access-and-above}

Para continuar a emitir licenças para conteúdo empacotado usando o Flash Media Rights Management Server (FMRMS) 1.0 ou 1.5, os dados de licença e política devem ser migrados do servidor LiveCycle ES para o novo servidor do cliente com base no SDK de acesso Adobe. As etapas importantes são:

1. Importando informações de licença
1. Conversão de políticas de FMRMS para o formato de Acesso Adobe
1. Para dar suporte às solicitações de compatibilidade 1.x por meio da `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`

Para importar informações de licença do LiveCycle ES para o servidor baseado no Adobe Access, consulte os exemplos de scripts de banco de dados fornecidos na [!DNL Reference Implementation\Server\migration\db] pasta. São fornecidos exemplos de scripts para exportar os dados relevantes de um banco de dados MySQL, Oracle ou SQL Server para um formato de arquivo CSV. Depois que os dados forem exportados, eles poderão ser importados para o banco de dados de sua escolha. As informações de licença exportadas incluem a ID de licença, uma ID de conteúdo atribuída no momento do empacotamento, a ID da política usada, o momento em que o conteúdo foi empacotado e a chave de criptografia do conteúdo. Para o Acesso ao Adobe, essas informações são necessárias para converter os metadados de conteúdo 1.x no formato de metadados de Acesso ao Adobe (consulte `FMRMSv1RequestHandler` e `FMRMSv1MetadataHandler`). Na implementação de referência, esses dados são armazenados na tabela do banco de dados Licença e usados por `RefImplMetadataConvReqHandler`.

As políticas existentes precisarão ser convertidas para o formato Adobe Access para usar essas políticas ao converter metadados e emitir licenças para conteúdo 1.0 ou 1.5. A pasta Reference Implementation\Server\migration contém códigos de exemplo para criar uma política de Acesso ao Adobe com base em políticas mais antigas.

Se você estiver migrando do FMRMS 1.0 para o Acesso ao Adobe, consulte a amostra V1_0PolicyConverter.java. Compile o código de amostra executando &quot; `ant-f build-migration.xml build-1.0-converter`&quot; (o script espera que as bibliotecas 1.0 e Adobe Access estejam em [!DNL libs/1.0] e libs/flashaccess, respectivamente). Edite o arquivo converter.properties para apontar para o servidor LiveCycle ES. Em seguida, execute &quot; `ant -f build-migration.xml migrate-all-1.0-policies`&quot; para converter todas as políticas do FMRMS 1.0 para o formato de Acesso Adobe.

Se você estiver migrando do FMRMS 1.5 para o Acesso ao Adobe, consulte a amostra V1_5PolicyConverter.java. Compile o código de amostra executando &quot; `ant-f build-migration.xml build-1.5-converter`&quot; (o script espera que as bibliotecas 1.5 e 3.0 estejam em libs/1.5 e libs/flashaccess, respectivamente). Edite o arquivo converter.properties para apontar para o servidor LiveCycle ES. Em seguida, execute &quot; `ant -f build-migration.xml migrate-all-1.5-policies`&quot; para converter todas as políticas de FMRMS 1.5 para o formato de Acesso Adobe.

As políticas convertidas serão gravadas em um conjunto de arquivos. Além disso, o PolicyConverter gerará um arquivo CSV contendo o mapeamento de IDs de política antigas para novas IDs de política. Este arquivo pode ser importado para a tabela &quot;PolicyConversion&quot; no banco de dados de implementação de referência e será usado por `RefImplMetadataConvReqHandler`.

Depois que os dados relevantes tiverem sido migrados para o servidor baseado em Acesso ao Adobe, você estará pronto para implementar o suporte às solicitações de compatibilidade 1.x. Consulte `RefImplUpgradeV1ClientHandler` e `RefImplMetadataConvReqHandler` na implementação de referência para obter exemplos de como processar esses tipos de solicitações.
