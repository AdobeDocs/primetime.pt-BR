---
seo-title: Manipulação de atualizações de certificados quando certificados emitidos por Adobe expiram
title: Manipulação de atualizações de certificados quando certificados emitidos por Adobe expiram
uuid: abc0ca3e-a78f-4078-9480-7116843cce05
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Processamento de atualizações de certificado quando certificados emitidos por Adobe expiram{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Talvez seja necessário obter um novo certificado do Adobe. Por exemplo, um certificado de produção expira quando um certificado de avaliação expira ou quando você muda de uma avaliação para um certificado de produção. Sempre que um certificado expirar e você não quiser reempacotar o conteúdo que usa o certificado antigo, você pode informar o License Server sobre os certificados antigos e os novos.

Para atualizar um servidor com novos certificados:

1. (Opcional) Quando você adiciona novas entradas a uma lista de atualização ou lista de revogação da política DRM existente, é necessário assinar com as novas credenciais e usar o certificado antigo para validar a assinatura no arquivo existente.

   Por exemplo, você pode usar a seguinte linha de comando para adicionar uma entrada a uma lista de atualização de política DRM existente, que foi assinada usando uma credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Opcional) Use a API Java para atualizar o servidor de licenças com a nova lista de atualização ou lista de revogação da política DRM:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   ou:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   Na implementação de referência, as propriedades usadas são `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Você também precisa atualizar o certificado usado para verificar as assinaturas: `RevocationList.verifySignature.X509Certificate`.

1. Atualize o servidor de licenças com os certificados novos e antigos.

   Se desejar consumir o conteúdo que foi empacotado usando os certificados antigos, verifique se o servidor de licenças tem acesso às credenciais do servidor de licenças novo e antigo, bem como às credenciais de transporte.

   Para obter as credenciais do servidor de licenças:

   * Verifique se a credencial atual foi passada para o construtor `LicenseHandler`:

      * Na implementação de referência, defina-a com a propriedade `LicenseHandler.ServerCredential`.
      * No Adobe Primetime DRM Server for Protected Streaming, a credencial atual deve ser a primeira credencial especificada no elemento `LicenseServerCredential` no arquivo flashaccess-locatário.xml.
   * Verifique se as credenciais atuais e antigas foram fornecidas para `AsymmetricKeyRetrieval`

      * Na implementação de referência, defina-a com as propriedades `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n`.

      * No Primetime DRM Server for Protected Streaming, as credenciais antigas são especificadas após a primeira credencial no elemento `LicenseServerCredential` no arquivo flashaccess-locatário.xml.

   Para as credenciais de transporte:

   * Verifique se a credencial atual foi passada para o método `HandlerConfiguration.setServerTransportCredential()`:

      * Na implementação de referência, defina-a com a propriedade `HandlerConfiguration.ServerTransportCredential`.
      * No Servidor DRM Primetime para streaming protegido, a credencial atual deve ser a primeira credencial especificada no elemento `TransportCredential` no arquivo [!DNL flashaccess-tenant.xml].
   * Verifique se as credenciais antigas foram fornecidas para `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Na implementação de referência, defina-a com as propriedades `HandlerConfiguration.AdditionalServerTransportCredential. n`.
      * No servidor DRM Primetime para streaming protegido, isso é especificado após a primeira credencial no elemento `TransportCredential` no arquivo flashaccess-Tennento.xml.




1. Atualize as ferramentas de empacotamento para garantir que elas estejam empacotando o conteúdo com as credenciais atuais. Certifique-se de que o certificado do servidor de licenças, o certificado de transporte e a credencial do empacotador mais recentes sejam usados para empacotamento.
1. Atualize o Certificado de Servidor de Licenças do Servidor de Chaves da seguinte forma:

   * Atualize as credenciais no arquivo de configuração do locatário do Adobe Primetime DRM Key Server, incluindo as credenciais antiga e nova do Key Server em flashaccess-keyserver-locatário.xml.
   * Verifique se o certificado atual foi passado para o método `HandlerConfiguration.setKeyServerCertificate()`.

      * Na implementação de referência, defina-a com a propriedade `HandlerConfiguration.KeyServerCertificate`.
      * No Primetime DRM Server for Protected Streaming, especifique o certificado do Key Server no elemento Configuration/Tenant/Certificados/KeyServer.

