---
description: Para atualizar um servidor compatível com a versão 3.0 do Servidor de licenças de implementação de referência ou com o Packager de pasta monitorada, é necessário substituir os arquivos .war que foram implantados em um Servidor de aplicativos pelos arquivos que foram incluídos no Servidor de implementação de referência do Adobe Primetime DRM.
title: Atualizar implantações existentes
exl-id: 83edaf0a-e527-470d-8b8d-23e5ba86b039
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Visão geral {#upgrade-existing-deployments-overview}

Para atualizar um servidor compatível com a versão 3.0 do Servidor de licenças de implementação de referência ou com o Packager de pasta monitorada, é necessário substituir os arquivos .war que foram implantados em um Servidor de aplicativos pelos arquivos que foram incluídos no Servidor de implementação de referência do Adobe Primetime DRM.

Para usar o registro de domínio com o Servidor de licenças de implementação de referência, várias novas tabelas de banco de dados são necessárias. Você precisa recriar todo o banco de dados de implementação de referência e executar `CreateSampleDB.sql`.

Para preservar registros do banco de dados e adicionar novas tabelas:

1. Abertura `CreateSampleDB.sql` e executar comandos que criam as seguintes tabelas:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Adicione as seguintes propriedades a [!DNL flashaccess-refimpl.properties] para usar o suporte de domínio:

   * `HandlerConfiguration.DomainCAs.n` ou `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` e `DomainRegistrationHandler.ServerCredential.password` ou `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Adicione as seguintes propriedades a [!DNL flashaccess-refimpl.properties] para oferecer suporte ao delivery remoto de chaves para clientes iOS:

   * `HandlerConfiguration.KeyServerCertificate` ou `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`
