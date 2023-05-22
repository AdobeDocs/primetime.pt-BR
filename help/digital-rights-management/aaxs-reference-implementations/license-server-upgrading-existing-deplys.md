---
title: Atualização de implantações existentes
description: Atualização de implantações existentes
copied-description: true
exl-id: e07b883f-d5f7-40d3-9221-a0dc2d859a5a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Atualização de implantações existentes {#upgrading-existing-deployments}

Para atualizar um servidor que esteja executando a versão 3.0 do Servidor de licenças de implementação de referência ou o Pacote de pastas monitoradas, substitua o [!DNL .war] Arquivos implantados no servidor de aplicativos com os arquivos incluídos no servidor de implementação de referência de acesso ao Adobe.

Se você planeja usar o registro de domínio com o Servidor de licenças de implementação de referência, várias novas tabelas de banco de dados são necessárias. Para recriar todo o banco de dados de implementação de referência, execute `CreateSampleDB.sql`. Para preservar os registros existentes do banco de dados e adicionar as novas tabelas, abra `CreateSampleDB.sql`e executar os comandos apenas para criar as seguintes tabelas:

* `DomainServerInfo`
* `DomainKeys`
* `DomainMembership`
* `UserDomainMembership`
* `UserDomainRefCount`

As seguintes propriedades devem ser adicionadas a flashaccess-refimpl.properties para usar o suporte do domínio:

* `HandlerConfiguration.DomainCAs.n` ou `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

* `Domain RegistrationHandler.ServerCredential` e `DomainRegistrationHandler.ServerCredential.password`ou `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

* `DomainRegistrationHandler.DomainServerUrl`

As seguintes propriedades devem ser adicionadas a [!DNL flashaccess-refimpl.properties] para oferecer suporte ao delivery remoto de chaves para clientes iOS:

* `HandlerConfiguration.KeyServerCertificate` ou `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
