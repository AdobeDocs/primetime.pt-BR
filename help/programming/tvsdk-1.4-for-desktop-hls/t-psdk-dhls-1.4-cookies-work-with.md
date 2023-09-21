---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
title: Trabalhar com cookies
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Trabalhar com cookies{#work-with-cookies}

Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.

Este é um exemplo com algum tipo de autenticação ao fazer solicitações ao servidor de chaves:

1. O cliente faz logon no site em um navegador e o logon mostra que tem permissão para visualizar o conteúdo.
1. Seu aplicativo gera um token de autenticação com base no que é esperado pelo servidor de licenças. Transmita esse valor para o TVSDK.
1. O TVSDK define esse valor no cabeçalho do cookie.
1. Quando o TVSDK faz uma solicitação ao servidor de chaves para obter uma chave para descriptografar o conteúdo, essa solicitação contém o valor de autenticação no cabeçalho do cookie, para que o servidor de chaves saiba que a solicitação é válida.

Para trabalhar com cookies:

1. Use o `cookieHeaders` propriedade no `NetworkConfiguration` para definir um cookie. A variável `cookieHeaders` é um objeto de Metadados, e você pode adicionar pares de valores chave a esse objeto para serem incluídos no cabeçalho do cookie.

   Por exemplo:

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   Por padrão, os cabeçalhos de cookies são enviados somente com solicitações de chave. Para enviar cabeçalhos de cookie com todas as solicitações, defina o `NetworkConfiguration` propriedade `useCookieHeadersForAllRequests` para verdadeiro.

1. Para assegurar que `NetworkConfiguration` funciona, defina-o como metadados:

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. Forneça os metadados da etapa anterior ao criar um `MediaResource`.

   Por exemplo, se você usar a variável `createFromURL` insira as seguintes informações:

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
