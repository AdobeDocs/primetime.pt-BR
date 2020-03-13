---
seo-title: Manipulação de atualizações de certificados quando seus certificados emitidos pela Adobe expiram
title: Manipulação de atualizações de certificados quando seus certificados emitidos pela Adobe expiram
uuid: 5151ef15-daf6-4fb3-bf83-25ebac1d003b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Manipulação de atualizações de certificados quando seus certificados emitidos pela Adobe expiram {#handling-certificate-updates-when-your-adobe-issued-certifcates-expire}

Pode ser que algumas vezes você precise obter um novo certificado da Adobe. Por exemplo, quando um certificado de produção expira, um certificado de avaliação expira ou quando você muda de uma avaliação para um certificado de produção. Quando um certificado expira e você não deseja reempacotar o conteúdo que usou o certificado antigo. Você pode tornar o License Server ciente dos certificados antigos e novos.

Use o procedimento a seguir para atualizar seu servidor com os novos certificados:

1. (Opcional) Ao adicionar novas entradas a uma lista de atualização de política existente ou a uma lista de revogação, certifique-se de assinar com as novas credenciais e usar o certificado antigo para validar a assinatura no arquivo existente.

   Por exemplo, use a seguinte linha de comando para adicionar uma entrada a uma lista de atualização de política existente, que foi assinada usando uma credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. Use a API Java para atualizar o servidor de licenças com a nova lista de atualização de política ou de revogação:

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

   * Verifique se a credencial atual foi passada para o `LicenseHandler` construtor:

      * Na implementação de referência, defina-a pela `LicenseHandler.ServerCredential` propriedade.
      * No Adobe Access Server for Protected Streaming, a credencial atual deve ser a primeira especificada no `LicenseServerCredential` elemento no arquivo flashaccess-locatário.xml.
   * Verifique se as credenciais atuais e antigas foram fornecidas para `AsymmetricKeyRetrieval`

      * Na implementação de referência, defina-a pelas propriedades `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n` .
      * No Adobe Access Server for Protected Streaming, as credenciais antigas são especificadas após a primeira credencial no `LicenseServerCredential` elemento no arquivo flashaccess-locatário.xml.
   Para as credenciais de transporte:

   * Verifique se a credencial atual foi passada para o `HandlerConfiguration.setServerTransportCredential()` método:

      * Na implementação de referência, defina-a pela `HandlerConfiguration.ServerTransportCredential` propriedade.
      * No Adobe Access Server para streaming protegido, a credencial atual deve ser a primeira especificada no `TransportCredential` elemento no arquivo flashaccess-locatário.xml.
   * Verifique se as credenciais antigas foram fornecidas para `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Na implementação de referência, defina-a pelas `HandlerConfiguration.AdditionalServerTransportCredential. n` propriedades.
      * No Adobe Access Server para streaming protegido, isso é especificado após a primeira credencial no `TransportCredential` elemento no arquivo flashaccess-locatário.xml.




1. Atualize as ferramentas de empacotamento para garantir que elas estejam empacotando o conteúdo com as credenciais atuais. Certifique-se de que o certificado do servidor de licenças, o certificado de transporte e a credencial do empacotador mais recentes sejam usados para empacotamento.
1. Para atualizar o Certificado do Servidor de Licenças do Servidor de Chaves:

   * Atualize as credenciais no arquivo de configuração do locatário do Adobe Access Key Server. Inclua as credenciais antigas e novas do Key Server em flashaccess-keyserver-locatário.xml.
   * Verifique se o certificado atual foi passado para o `HandlerConfiguration.setKeyServerCertificate()` método.

      * Na implementação de referência, defina-a pela `HandlerConfiguration.KeyServerCertificate` propriedade.
      * No Adobe Access Server for Protected Streaming, especifique o certificado do Key Server no elemento Configuração/Locatário/Certificados/KeyServer.

