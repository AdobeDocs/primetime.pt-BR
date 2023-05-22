---
title: Manipulação de atualizações de certificado quando os certificados emitidos pelo Adobe expiram
description: Manipulação de atualizações de certificado quando os certificados emitidos pelo Adobe expiram
copied-description: true
exl-id: 9051a647-87ed-4df6-8bbc-bb5c112383ee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Manipulação de atualizações de certificado quando os certificados emitidos pelo Adobe expiram{#handling-certificate-updates-when-adobe-issued-certificates-expire}

Talvez seja necessário obter um novo certificado do Adobe. Por exemplo, um certificado de produção expira quando um certificado de avaliação expira ou quando você muda de uma avaliação para um certificado de produção. Sempre que um certificado expirar e você não quiser reempacotar o conteúdo que usa o certificado antigo, poderá tornar o License Server ciente dos certificados antigos e novos.

Para atualizar um servidor com novos certificados:

1. (Opcional) Quando você adiciona novas entradas a uma lista de atualização ou revogação de política DRM existente, é necessário assinar com as novas credenciais e usar o certificado antigo para validar a assinatura no arquivo existente.

   Por exemplo, você pode usar a seguinte linha de comando para adicionar uma entrada a uma lista de atualização de política DRM existente, que foi assinada usando uma credencial diferente:

   ```
   java -jar AdobePolicyUpdateListManager.jar newList -f oldList oldSigningCert.cer -u pol 0 "" ""
   ```

1. (Opcional) Use a API do Java para atualizar o servidor de licenças com a nova lista de atualização ou revogação de política DRM:

   ```
   HandlerConfiguration.setRevocationList() 
   ```

   ou:

   ```
   HandlerConfiguration.setPolicyUpdateList()
   ```

   Na implementação de referência, as propriedades usadas são `HandlerConfiguration.RevocationList` e `HandlerConfiguration.PolicyUpdateList`. Você também precisa atualizar o certificado usado para verificar as assinaturas: `RevocationList.verifySignature.X509Certificate`.

1. Atualize o servidor de licenças com os certificados novos e antigos.

   Se quiser consumir conteúdo que foi empacotado usando os certificados antigos, verifique se o servidor de licenças tem acesso às credenciais de servidor de licenças antigas e novas, bem como às credenciais de transporte.

   Para as credenciais do servidor de licenças:

   * Certifique-se de que a credencial atual seja passada para o `LicenseHandler` construtor:

      * Na implementação de referência, defina-a com o `LicenseHandler.ServerCredential` propriedade.
      * No Servidor DRM da Adobe Primetime para Transmissão Protegida, a credencial atual deve ser a primeira credencial especificada no `LicenseServerCredential` elemento no arquivo flashaccess-tenant.xml.
   * Verifique se as credenciais atuais e antigas foram fornecidas para o `AsymmetricKeyRetrieval`

      * Na implementação de referência, defina-a com o `LicenseHandler.ServerCredential` e `AsymmetricKeyRetrieval.ServerCredential. n` propriedades.

      * No Servidor DRM Primetime para Transmissão Protegida, as credenciais antigas são especificadas após a primeira credencial no `LicenseServerCredential` elemento no arquivo flashaccess-tenant.xml.
   Para as credenciais de transporte:

   * Certifique-se de que a credencial atual seja passada para o `HandlerConfiguration.setServerTransportCredential()` método:

      * Na implementação de referência, defina-a com o `HandlerConfiguration.ServerTransportCredential` propriedade.
      * No Servidor DRM Primetime para transmissão protegida, a credencial atual deve ser a primeira especificada no `TransportCredential` elemento na [!DNL flashaccess-tenant.xml] arquivo.
   * Verifique se as credenciais antigas foram fornecidas para `HandlerConfiguration.setAdditionalServerTransportCredentials`():

      * Na implementação de referência, defina-a com o `HandlerConfiguration.AdditionalServerTransportCredential. n` propriedades.
      * No Servidor DRM Primetime para transmissão protegida, isso é especificado após a primeira credencial no `TransportCredential` elemento no arquivo flashaccess-tenant.xml.




1. Atualize as ferramentas de empacotamento para garantir que elas estejam empacotando o conteúdo com as credenciais atuais. Verifique se o certificado do servidor de licenças, o certificado de transporte e a credencial do empacotador mais recentes são usados para empacotamento.
1. Atualize o certificado do servidor de licenças do servidor de chaves da seguinte maneira:

   * Atualize as credenciais no arquivo de configuração do locatário do Adobe Primetime DRM Key Server incluindo as credenciais do Servidor de Chaves antigas e novas em flashaccess-keyserver-tenant.xml.
   * Certifique-se de que o certificado atual seja passado para o `HandlerConfiguration.setKeyServerCertificate()` método.

      * Na implementação de referência, defina-a com o `HandlerConfiguration.KeyServerCertificate` propriedade.
      * No Servidor DRM do Primetime para Streaming Protegido, especifique o certificado do Servidor de Chaves no por meio do elemento Configuration/Tenant/Certificates/KeyServer.
