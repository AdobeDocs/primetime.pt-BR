---
seo-title: Processamento de atualizações de certificado quando seus certificados emitidos por Adobe expiram
title: Processamento de atualizações de certificado quando seus certificados emitidos por Adobe expiram
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Processando atualizações de certificado quando seus certificados emitidos por Adobe expiram {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Pode haver momentos em que você tenha que obter um novo certificado do Adobe. Por exemplo, quando um certificado de produção expira, um certificado de avaliação expira ou quando você muda de uma avaliação para um certificado de produção. Quando um certificado expira e você não deseja reempacotar o conteúdo que usou o certificado antigo. Você pode tornar o License Server ciente dos certificados antigos e novos.

Use o procedimento a seguir para atualizar seu servidor com os novos certificados:

1. (Opcional) Ao adicionar novas entradas a uma lista de atualização ou lista de revogação de política existente, certifique-se de assinar com as novas credenciais e usar o certificado antigo para validar a assinatura no arquivo existente.

   Por exemplo, use a seguinte linha de comando para adicionar uma entrada a uma lista de atualização de política existente, que foi assinada usando uma credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Use a API Java para atualizar o servidor de licenças com a nova lista de atualização de política ou lista de revogação:

   ```
    HandlerConfiguration.setRevocationList() 
   ```

   ou:

   ```
    HandlerConfiguration.setPolicyUpdateList()
   ```

   Na implementação de referência, as propriedades usadas são `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Atualize também o certificado usado para verificar as assinaturas: `RevocationList.verifySignature.X509Certificate`.

1. Para consumir conteúdo que foi empacotado usando os certificados antigos, o servidor de licenças exige as credenciais do servidor de licenças antigo e novo e as credenciais de transporte. Atualize o servidor de licenças com os certificados novos e antigos.

   Para obter as credenciais do servidor de licenças:

   * Verifique se a credencial atual foi passada para o construtor `LicenseHandler`:

      * Na implementação de referência, defina-a pela propriedade `LicenseHandler.ServerCredential`.
      * No Adobe Access Server for Protected Streaming, a credencial atual deve ser a primeira credencial especificada no elemento `LicenseServerCredential` no arquivo flashaccess-locatário.xml.
   * Verifique se as credenciais atuais e antigas foram fornecidas para `AsymmetricKeyRetrieval`

      * Na implementação de referência, defina-a pelas propriedades `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n`.
      * No Adobe Access Server for Protected Streaming, as credenciais antigas são especificadas após a primeira credencial no elemento `LicenseServerCredential` no arquivo flashaccess-locatário.xml.

   Para as credenciais de transporte:

   * Verifique se a credencial atual foi passada para o método `HandlerConfiguration.setServerTransportCredential()`:

      * Na implementação de referência, defina-a pela propriedade `HandlerConfiguration.ServerTransportCredential`.
      * No Adobe Access Server para streaming protegido, a credencial atual deve ser a primeira credencial especificada no elemento `TransportCredential` no arquivo flashaccess-locatário.xml.
   * Verifique se as credenciais antigas foram fornecidas para `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Na implementação de referência, defina-a pelas propriedades `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * No Adobe Access Server para streaming protegido, isso é especificado após a primeira credencial no elemento `TransportCredential` no arquivo flashaccess-locatário.xml.




1. Atualize as ferramentas de empacotamento para garantir que elas estejam empacotando o conteúdo com as credenciais atuais. Certifique-se de que o certificado do servidor de licenças, o certificado de transporte e a credencial do empacotador mais recentes sejam usados para empacotamento.
1. Para atualizar o Certificado do Servidor de Licenças do Servidor de Chaves:

   * Atualize as credenciais no arquivo de configuração do locatário do Servidor de Chaves de Acesso ao Adobe. Inclua as credenciais antigas e novas do Key Server em flashaccess-keyserver-locatário.xml.
   * Verifique se o certificado atual foi passado para o método `HandlerConfiguration.setKeyServerCertificate()`.

      * Na implementação de referência, defina-a pela propriedade `HandlerConfiguration.KeyServerCertificate`.
      * No Adobe Access Server for Protected Streaming, especifique o certificado do Key Server no elemento Configuration/Tenant/Certificados/KeyServer.

