---
title: Lidar com atualizações de certificados quando os certificados emitidos pelo Adobe expiram
description: Lidar com atualizações de certificados quando os certificados emitidos pelo Adobe expiram
copied-description: true
exl-id: 9768544e-7e92-4c3a-9863-af9aed74a0c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Lidar com atualizações de certificados quando os certificados emitidos pelo Adobe expiram {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Pode haver momentos em que você precise obter um novo certificado do Adobe. Por exemplo, quando um certificado de produção expira, um certificado de avaliação expira ou quando você muda de uma avaliação para um certificado de produção. Quando um certificado expira e você não deseja reempacotar o conteúdo que usou o certificado antigo. Você pode tornar o License Server ciente dos certificados antigos e novos.

Use o procedimento a seguir para atualizar seu servidor com os novos certificados:

1. (Opcional) Ao adicionar novas entradas a uma lista de atualização ou revogação de política existente, certifique-se de assinar com as novas credenciais e usar o certificado antigo para validar a assinatura no arquivo existente.

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

   Na implementação de referência, as propriedades que você usa são `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Atualize também o certificado usado para verificar as assinaturas: `RevocationList.verifySignature.X509Certificate`.

1. Para consumir conteúdo que foi empacotado usando os certificados antigos, o servidor de licenças requer as credenciais de servidor de licenças antigas e novas e as credenciais de transporte. Atualize o servidor de licenças com os certificados novos e antigos.

   Para as credenciais do servidor de licenças:

   * Certifique-se de que a credencial atual seja passada para o `LicenseHandler` construtor:

      * Na implementação de referência, defina-a por meio da variável `LicenseHandler.ServerCredential` propriedade.
      * No Adobe Access Server para Protected Streaming, a credencial atual deve ser a primeira credencial especificada no `LicenseServerCredential` elemento no arquivo flashaccess-tenant.xml.
   * Verifique se as credenciais atuais e antigas foram fornecidas para o `AsymmetricKeyRetrieval`

      * Na implementação de referência, defina-a por meio da variável `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n` propriedades.
      * No Adobe Access Server para Protected Streaming, as credenciais antigas são especificadas após a primeira credencial no `LicenseServerCredential` elemento no arquivo flashaccess-tenant.xml.
   Para as credenciais de transporte:

   * Certifique-se de que a credencial atual seja passada para o `HandlerConfiguration.setServerTransportCredential()` método:

      * Na implementação de referência, defina-a por meio da variável `HandlerConfiguration.ServerTransportCredential` propriedade.
      * No Adobe Access Server para transmissão protegida, a credencial atual deve ser a primeira especificada no `TransportCredential` elemento no arquivo flashaccess-tenant.xml.
   * Verifique se as credenciais antigas foram fornecidas para `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Na implementação de referência, defina-a por meio da variável `HandlerConfiguration.AdditionalServerTransportCredential. n` propriedades.
      * No Adobe Access Server para transmissão protegida, isso é especificado após a primeira credencial no `TransportCredential` elemento no arquivo flashaccess-tenant.xml.




1. Atualize as ferramentas de empacotamento para garantir que elas estejam empacotando o conteúdo com as credenciais atuais. Verifique se o certificado do servidor de licenças, o certificado de transporte e a credencial do empacotador mais recentes são usados para empacotamento.
1. Para atualizar o Certificado de servidor de licença do servidor de chaves:

   * Atualize as credenciais no arquivo de configuração do locatário do Adobe Access Key Server. Inclua as credenciais do Servidor de Chaves antigas e novas em flashaccess-keyserver-tenant.xml.
   * Verifique se o certificado atual é passado para o `HandlerConfiguration.setKeyServerCertificate()` método.

      * Na implementação de referência, defina-a por meio da variável `HandlerConfiguration.KeyServerCertificate` propriedade.
      * No Adobe Access Server para transmissão protegida, especifique o certificado do servidor de chaves no por meio do elemento Configuration/Tenant/Certificates/KeyServer.
