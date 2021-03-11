---
title: Manipular atualizações de certificado quando os certificados emitidos por Adobe expirarem
description: Manipular atualizações de certificado quando os certificados emitidos por Adobe expirarem
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Lidar com atualizações de certificado quando seus certificados emitidos por Adobe expiram {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Pode haver momentos em que você precise obter um novo certificado do Adobe. Por exemplo, quando um certificado de produção expira, um certificado de avaliação expira ou você muda de uma avaliação para um certificado de produção. Quando um certificado expira e você não deseja reempacotar o conteúdo que usou o certificado antigo. Você pode tornar o License Server ciente dos certificados antigos e novos.

Use o procedimento a seguir para atualizar seu servidor com os novos certificados:

1. (Opcional) Ao adicionar novas entradas a uma lista de atualização de política ou lista de revogação existente, certifique-se de assinar com as novas credenciais e usar o certificado antigo para validar a assinatura no arquivo existente.

   Por exemplo, use a seguinte linha de comando para adicionar uma entrada a uma lista de atualização de política existente, que foi assinada usando uma credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Use a API do Java para atualizar o servidor de licenças com a nova lista de atualização de política ou lista de revogação:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   ou:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   Na implementação de referência, as propriedades usadas são `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Atualize também o certificado usado para verificar as assinaturas: `RevocationList.verifySignature.X509Certificate`.

1. Para consumir conteúdo que foi empacotado usando os certificados antigos, o servidor de licenças requer as credenciais do servidor de licenças novo e antigo e as credenciais de transporte. Atualize o servidor de licenças com os certificados novos e antigos.

   Para as credenciais do servidor de licenças:

   * Verifique se a credencial atual foi passada para o construtor `LicenseHandler`:

      * Na implementação de referência, defina-a pela propriedade `LicenseHandler.ServerCredential`.
      * No Adobe Access Server para transmissão protegida, a credencial atual deve ser a primeira credencial especificada no elemento `LicenseServerCredential` no arquivo flashaccess-tenant.xml.
   * Certifique-se de que as credenciais atuais e antigas sejam fornecidas para `AsymmetricKeyRetrieval`

      * Na implementação de referência, defina-a pelas propriedades `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n`.
      * No Adobe Access Server for Protected Streaming, as credenciais antigas são especificadas após a primeira credencial no elemento `LicenseServerCredential` no arquivo flashaccess-tenant.xml.

   Para as credenciais de transporte:

   * Verifique se a credencial atual foi passada para o método `HandlerConfiguration.setServerTransportCredential()`:

      * Na implementação de referência, defina-a pela propriedade `HandlerConfiguration.ServerTransportCredential`.
      * No Adobe Access Server para transmissão protegida, a credencial atual deve ser a primeira credencial especificada no elemento `TransportCredential` no arquivo flashaccess-tenant.xml.
   * Certifique-se de que as credenciais antigas sejam fornecidas a `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Na implementação de referência, defina-a pelas propriedades `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * No Adobe Access Server para transmissão protegida, isso é especificado após a primeira credencial no elemento `TransportCredential` no arquivo flashaccess-tenant.xml .




1. Atualize as ferramentas de empacotamento para garantir que elas estejam empacotando o conteúdo com as credenciais atuais. Certifique-se de que o certificado do servidor de licenças, o certificado de transporte e a credencial do empacotador mais recentes sejam usados para empacotamento.
1. Para atualizar o certificado do servidor de licenças do servidor de chaves:

   * Atualize as credenciais no arquivo de configuração do locatário do Adobe Access Key Server. Inclua as credenciais antigas e novas do Servidor-chave em flashaccess-keyserver-tenant.xml.
   * Verifique se o certificado atual foi passado para o método `HandlerConfiguration.setKeyServerCertificate()`.

      * Na implementação de referência, defina-a pela propriedade `HandlerConfiguration.KeyServerCertificate`.
      * No Adobe Access Server for Protected Streaming, especifique o certificado do Servidor de Chave no por meio do elemento Configuration/Tenant/Certificates/KeyServer .

