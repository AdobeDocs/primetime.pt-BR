---
description: Para atualizar um servidor que suporta o License Server de Implementação de Referência 3.0 ou o Watched Folder Packager, é necessário substituir os arquivos .war que foram implantados em um Servidor de Aplicativos pelos arquivos que foram incluídos com o Servidor de Implementação de Referência do Adobe Primetime DRM.
title: Atualizar implantações existentes
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Visão geral {#upgrade-existing-deployments-overview}

Para atualizar um servidor que suporta o License Server de Implementação de Referência 3.0 ou o Watched Folder Packager, é necessário substituir os arquivos .war que foram implantados em um Servidor de Aplicativos pelos arquivos que foram incluídos com o Servidor de Implementação de Referência do Adobe Primetime DRM.

Para usar o registro de domínio no Servidor de Licença de Implementação de Referência, são necessárias várias novas tabelas de banco de dados. Você precisa recriar todo o banco de dados de implementação de referência e executar `CreateSampleDB.sql`.

Para preservar registros de banco de dados e adicionar novas tabelas:

1. Abra `CreateSampleDB.sql` e execute comandos que criem as seguintes tabelas:

   * `DomainServerInfo`
   * `DomainKeys`
   * `DomainMembership`
   * `UserDomainMembership`
   * `UserDomainRefCount`

1. Adicione as seguintes propriedades a [!DNL flashaccess-refimpl.properties] para usar o suporte de domínio:

   * `HandlerConfiguration.DomainCAs.n` ou  `RefImpl.HSM.HandlerConfiguration.DomainCAs.Alias.n`

   * `Domain RegistrationHandler.ServerCredential` e  `DomainRegistrationHandler.ServerCredential.password` ou  `RefImpl.HSM.DomainRegistrationHandler.ServerCredential.Alias`

   * `DomainRegistrationHandler.DomainServerUrl`

1. Adicione as seguintes propriedades a [!DNL flashaccess-refimpl.properties] para oferecer suporte à entrega de chaves remotas aos clientes do iOS:

   * `HandlerConfiguration.KeyServerCertificate` ou  `RefImpl.HSM.HandlerConfiguration.KeyServerCertificate.Alias`