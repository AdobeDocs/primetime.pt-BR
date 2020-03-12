---
description: Para atualizar um servidor compatível com a versão 3.0 do Reference Implementation License Server ou com o Watched Folder Packager, é necessário substituir os arquivos .war que foram implantados em um servidor de aplicativos pelos arquivos que foram incluídos no Adobe Primetime DRM Reference Implementation Server.
seo-description: Para atualizar um servidor compatível com a versão 3.0 do Reference Implementation License Server ou com o Watched Folder Packager, é necessário substituir os arquivos .war que foram implantados em um servidor de aplicativos pelos arquivos que foram incluídos no Adobe Primetime DRM Reference Implementation Server.
seo-title: Atualizar implantações existentes
title: Atualizar implantações existentes
uuid: 1a40aae9-f639-41fa-b42d-cf8cdfcde694
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Visão geral {#upgrade-existing-deployments-overview}

Para atualizar um servidor compatível com a versão 3.0 do Reference Implementation License Server ou com o Watched Folder Packager, é necessário substituir os arquivos .war que foram implantados em um servidor de aplicativos pelos arquivos que foram incluídos no Adobe Primetime DRM Reference Implementation Server.

Para usar o registro de domínio com o Servidor de Licenças de Implementação de Referência, são necessárias várias novas tabelas de banco de dados. É necessário recriar o banco de dados de implementação de referência inteiro e executar `CreateSampleDB.sql`.

Para preservar os registros do banco de dados e adicionar novas tabelas:

1. Abra `CreateSampleDB.sql` e execute comandos que criem as seguintes tabelas:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Adicione as seguintes propriedades para usar [!DNL flashaccess-refimpl.properties] o suporte de domínio:

   * `HandlerConfiguration.DomainCAs.n` ou `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` e `DomainRegistrationHandler.ServerCredential.password` ou `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Adicione as seguintes propriedades [!DNL flashaccess-refimpl.properties] para oferecer suporte à entrega de chave remota para clientes iOS:

   * `HandlerConfiguration.KeyServerCertificate` ou `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`