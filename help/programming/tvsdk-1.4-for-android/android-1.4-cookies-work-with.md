---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
seo-description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
seo-title: Trabalhar com cookies
title: Trabalhar com cookies
uuid: f060b520-ceec-48ca-929f-683566fe6ae7
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---


# Trabalhar com cookies{#work-with-cookies}

Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.

Este é um exemplo com algum tipo de autenticação ao fazer solicitações ao servidor de chaves:

1. Seu cliente entra em seu site em um navegador e seu login mostra que ele tem permissão para visualização de conteúdo.
1. Seu aplicativo gera um token de autenticação, com base no que é esperado pelo servidor de licenças. Passe esse valor para TVSDK.
1. O TVSDK define esse valor no cabeçalho do cookie.
1. Quando o TVSDK faz uma solicitação ao servidor de chaves para obter uma chave para descriptografar o conteúdo, essa solicitação contém o valor de autenticação no cabeçalho do cookie, de modo que o servidor de chaves saiba que a solicitação é válida.

Para trabalhar com cookies:

1. Crie um `cookieManager` e adicione seus cookies para os URIs a seu `cookieStore`.

   Por exemplo:

   >[!IMPORTANT]
   >
   >Quando o redirecionamento 302 estiver ativado, a solicitação de anúncio poderá ser redirecionada para um domínio diferente do domínio ao qual o cookie pertence.

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   O TVSDK query este cookieManager em tempo de execução, verifica se há cookies associados ao URL e os usa automaticamente.

   Outra opção é usar `cookieHeaders` em `NetworkConfiguration` para definir uma string de cabeçalho de cookie arbitrária a ser usada para solicitações. Por padrão, esse cabeçalho de cookie é enviado somente com solicitações de chave. Para enviar o cabeçalho do cookie com todas as solicitações, use o método `NetworkConfiguration` `setUseCookieHeadersForAllRequests`:

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
