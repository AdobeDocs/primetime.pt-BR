---
title: Atualização das implantações existentes
description: Atualização das implantações existentes
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Atualizar implantações existentes {#upgrading-existing-deployments}

Para atualizar um servidor executando o Servidor de Licenças de Implementação de Referência versão 3.0 ou o Empacotador de Pastas Assistidas, substitua os arquivos [!DNL .war] implantados em seu Servidor de Aplicativos pelos arquivos incluídos no Servidor de Implementação de Referência de Acesso ao Adobe.

Se você planeja usar o registro de domínio com o Servidor de Licenças de Implementação de Referência, várias novas tabelas de banco de dados são necessárias. Para recriar todo o banco de dados de implementação de referência, execute `CreateSampleDB.sql`. Para preservar os registros de banco de dados existentes e adicionar as novas tabelas, abra `CreateSampleDB.sql`e execute apenas os comandos para criar as seguintes tabelas:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

As seguintes propriedades devem ser adicionadas a flashaccess-refimpl.properties para usar o suporte ao domínio:

* `HandlerConfiguration.DomainCAs.n` ou  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` e  `DomainRegistrationHandler.ServerCredential.password`ou  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

As seguintes propriedades devem ser adicionadas a [!DNL flashaccess-refimpl.properties] para suportar a entrega de chaves remotas aos clientes do iOS:

* `HandlerConfiguration.KeyServerCertificate` ou  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`

