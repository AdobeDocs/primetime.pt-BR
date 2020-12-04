---
seo-title: Atualização de implantações existentes
title: Atualização de implantações existentes
uuid: 57e62a88-e541-435c-8274-7f1602548601
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Atualizando implantações existentes {#upgrading-existing-deployments}

Para atualizar um servidor executando a versão 3.0 do Servidor de Licença de Implementação de Referência ou o Watched Folder Packager, substitua os arquivos [!DNL .war] implantados no Servidor de Aplicativos pelos arquivos incluídos no Servidor de Implementação de Referência de Adobe Access.

Se você planeja usar o registro de domínio com o Servidor de Licenças de Implementação de Referência, várias novas tabelas de banco de dados serão necessárias. Para recriar todo o banco de dados de implementação de referência, execute `CreateSampleDB.sql`. Para preservar os registros existentes do banco de dados e adicionar as novas tabelas, abra `CreateSampleDB.sql`e execute apenas os comandos para criar as seguintes tabelas:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

As seguintes propriedades devem ser adicionadas a flashaccess-refimpl.properties para usar o suporte ao domínio:

* `HandlerConfiguration.DomainCAs.n` ou  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` e  `DomainRegistrationHandler.ServerCredential.password`ou  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

As seguintes propriedades devem ser adicionadas a [!DNL flashaccess-refimpl.properties] para oferecer suporte ao delivery de chave remota para clientes iOS:

* `HandlerConfiguration.KeyServerCertificate` ou  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

