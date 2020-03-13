---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
seo-description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
seo-title: Trabalhar com cookies
title: Trabalhar com cookies
uuid: 7586a5a7-9914-403b-86a9-fbdd28664b07
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Trabalhar com cookies{#work-with-cookies}

Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.

Este é um exemplo com algum tipo de autenticação ao fazer solicitações ao servidor de chaves:

1. Seu cliente entra em seu site em um navegador e seu login mostra que ele tem permissão para exibir o conteúdo.
1. Seu aplicativo gera um token de autenticação, com base no que é esperado pelo servidor de licenças. Passe esse valor para TVSDK.
1. O TVSDK define esse valor no cabeçalho do cookie.
1. Quando o TVSDK faz uma solicitação ao servidor de chaves para obter uma chave para descriptografar o conteúdo, essa solicitação contém o valor de autenticação no cabeçalho do cookie, de modo que o servidor de chaves saiba que a solicitação é válida.

Para trabalhar com cookies:

1. Use a `cookieHeaders` propriedade em `NetworkConfiguration` para definir um cookie. A `cookieHeaders` propriedade é um objeto de Metadados, e você pode adicionar pares de valores chave a esse objeto para serem incluídos no cabeçalho do cookie.

   Por exemplo:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   Por padrão, os cabeçalhos de cookies são enviados somente com solicitações principais. Para enviar cabeçalhos de cookies com todas as solicitações, defina a `NetworkConfiguration` propriedade como true `useCookieHeadersForAllRequests` .

1. Para garantir que `NetworkConfiguration` funcione, defina-o como metadados:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Forneça os metadados da etapa anterior ao criar um `MediaResource`.

   Por exemplo, se você usar o `createFromURL` método, insira as seguintes informações:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

