---
title: Manipulação de atualizações de certificado quando certificados emitidos por Adobe expiram
description: Manipulação de atualizações de certificado quando certificados emitidos por Adobe expiram
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Lidar com atualizações de certificado quando certificados emitidos por Adobe expirarem{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Talvez seja necessário obter um novo certificado do Adobe. Por exemplo, um certificado de produção expira quando um certificado de avaliação expira ou quando você muda de uma avaliação para um certificado de produção. Sempre que um certificado expirar e você não quiser reempacotar o conteúdo que usa o certificado antigo, é possível tornar o License Server ciente dos certificados antigos e novos.

Para atualizar um servidor com novos certificados:

1. (Opcional) Ao adicionar novas entradas a uma lista de atualização ou revogação de política de DRM existente, é necessário assinar com as novas credenciais e usar o certificado antigo para validar a assinatura no arquivo existente.

   Por exemplo, você pode usar a seguinte linha de comando para adicionar uma entrada a uma lista de atualização de política de DRM existente, que foi assinada usando uma credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Opcional) Use a API do Java para atualizar o servidor de licenças com a nova lista de atualização ou lista de revogação da política de DRM:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   ou:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   Na implementação de referência, as propriedades usadas são `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Você também precisa atualizar o certificado usado para verificar as assinaturas: `RevocationList.verifySignature.X509Certificate`.

1. Atualize o servidor de licenças com os certificados novos e antigos.

   Se quiser consumir conteúdo que foi empacotado usando os certificados antigos, verifique se o servidor de licenças tem acesso às credenciais do servidor de licenças novo e antigo, bem como às credenciais de transporte.

   Para as credenciais do servidor de licenças:

   * Verifique se a credencial atual foi passada para o construtor `LicenseHandler`:

      * Na implementação de referência, defina-a com a propriedade `LicenseHandler.ServerCredential` .
      * No Adobe Primetime DRM Server for Protected Streaming, a credencial atual deve ser a primeira credencial especificada no elemento `LicenseServerCredential` no arquivo flashaccess-tenant.xml.
   * Certifique-se de que as credenciais atuais e antigas sejam fornecidas para `AsymmetricKeyRetrieval`

      * Na implementação de referência, defina-a com as propriedades `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n`.

      * No Servidor DRM Primetime para Transmissão Protegida, as credenciais antigas são especificadas após a primeira credencial no elemento `LicenseServerCredential` no arquivo flashaccess-tenant.xml.

   Para as credenciais de transporte:

   * Verifique se a credencial atual foi passada para o método `HandlerConfiguration.setServerTransportCredential()`:

      * Na implementação de referência, defina-a com a propriedade `HandlerConfiguration.ServerTransportCredential` .
      * No Servidor DRM Primetime para transmissão protegida, a credencial atual deve ser a primeira credencial especificada no elemento `TransportCredential` no arquivo [!DNL flashaccess-tenant.xml].
   * Certifique-se de que as credenciais antigas sejam fornecidas a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Na implementação de referência, defina-a com as propriedades `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * No servidor DRM Primetime para transmissão protegida, isso é especificado após a primeira credencial no elemento `TransportCredential` no arquivo flashaccess-tenant.xml .




1. Atualize as ferramentas de empacotamento para garantir que elas estejam empacotando o conteúdo com as credenciais atuais. Certifique-se de que o certificado do servidor de licenças, o certificado de transporte e a credencial do empacotador mais recentes sejam usados para empacotamento.
1. Atualize o Certificado do Servidor de Licenças do Servidor de Chave da seguinte maneira:

   * Atualize as credenciais no arquivo de configuração do locatário do Adobe Primetime DRM Key Server incluindo as credenciais antigas e novas do Key Server em flashaccess-keyserver-tenant.xml.
   * Verifique se o certificado atual foi passado para o método `HandlerConfiguration.setKeyServerCertificate()`.

      * Na implementação de referência, defina-a com a propriedade `HandlerConfiguration.KeyServerCertificate` .
      * No Servidor DRM Primetime para Transmissão Protegida, especifique o certificado do Servidor de Chave no através do elemento Configuration/Tenant/Certificates/KeyServer .

