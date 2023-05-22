---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
title: Trabalhar com cookies
exl-id: 7482777a-c338-4e0d-b123-ce2712657b8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
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

1. Criar um `cookieManager` e adicione seus cookies para os URIs ao seu `cookieStore`.

   Por exemplo:

   >[!IMPORTANT]
   >
   >Quando o redirecionamento 302 está ativado, a solicitação de anúncio pode ser redirecionada para um domínio diferente do domínio ao qual o cookie pertence.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   O TVSDK consulta esse cookieManager no tempo de execução, verifica se há cookies associados ao URL e os usa automaticamente.

   Outra opção é usar `cookieHeaders` in `NetworkConfiguration` para definir uma string de cabeçalho de cookie arbitrária a ser usada para solicitações. Por padrão, esse cabeçalho de cookie é enviado somente com solicitações de chave. Para enviar o cabeçalho do cookie com todas as solicitações, use o `NetworkConfiguration` método `setUseCookieHeadersForAllRequests`:

```java
   NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
    
   Metadata cookie = new MetadataNode(); 
   cookie.setValue("reqPayload", “1234567”); 
   networkConfiguration.setCookieHeaders(cookie); 
   networkConfiguration.setUseCookieHeadersForAllRequests( true ); 
    
   // Set NetworkConfiguration as Metadata:                                                                   
   MetadataNode resourceMetadata = new MetadataNode(); 
   resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                            networkConfiguration); 
    
   // Call MediaResource.createFromURL to set the metadata: 
   MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
   // Load the resource 
   mediaPlayer.replaceCurrentItem(resource);
```
