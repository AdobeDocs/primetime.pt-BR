---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessões, acesso à porta e assim por diante.
title: Trabalhar com cookies
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---


# Trabalhar com cookies {#work-with-cookies}

Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessões, acesso à porta e assim por diante.

Esta é uma amostra de solicitação para o servidor de chaves com algumas autenticações:

1. O cliente entra no site em um navegador e o logon mostra que esse cliente tem permissão para visualizar o conteúdo.
1. Com base no que é esperado pelo servidor de licenças, seu aplicativo gera um token de autenticação.

   Esse valor é passado para TVSDK.
1. O TVSDK define esse valor no cabeçalho do cookie.
1. Quando o TVSDK faz uma solicitação ao servidor de chaves para obter uma chave para descriptografar o conteúdo, a solicitação contém o valor de autenticação no cabeçalho do cookie.

   O servidor de chaves sabe que a solicitação é válida.

Para trabalhar com cookies:

1. Crie um `cookieManager` e adicione seus cookies para os URIs ao cookieStore.

   Por exemplo:

   ```java
   CookieManager cookieManager=new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   >[!TIP]
   >
   >Quando o redirecionamento 302 é ativado, a solicitação de anúncio pode ser redirecionada para um domínio diferente do domínio ao qual o cookie pertence.

   O TVSDK consulta esse `cookieManager` no tempo de execução, verifica se há cookies associados ao URL e usa esses cookies automaticamente.

   Se os cookies precisarem ser atualizados no aplicativo durante a reprodução, não use a API `networkConfiguration.setCookieHeaders`, pois a atualização ocorrerá no armazenamento de cookies JAVA.

   `networkConfiguration.setCookieHeaders` A API define os cookies como C++ CookieStore do TVSDK.

   Ao usar cookies JAVA e compartilhá-los entre Aplicativo e TVSDK, use o CookieStore JAVA para gerenciar os cookies exclusivamente.

   Antes de inicializar a reprodução, defina os cookies como CookieStore usando o Gerenciador de cookies, como mencionado acima.

   O cookie armazenado no CookieStore será automaticamente selecionado pelo TVSDK.

   Se um valor de cookie precisar ser atualizado posteriormente durante a reprodução, chame o mesmo método de adição de CookieStore com a mesma chave e um novo campo de valor.

   Também definido
   `networkConfiguration.setReadSetCookieHeader`(false) antes de chamar
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >Depois de definir esse &#39;setReadSetCookieHeader&#39; como falso, defina os cookies para as solicitações principais usando o gerenciador de cookies JAVA.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Essa API de retorno de chamada será acionada sempre que houver uma atualização em cookies C++ (cookies que vêm da resposta http). O aplicativo precisa ouvir esse retorno de chamada e pode atualizar seu CookieStore JAVA de acordo, para que suas chamadas de rede no JAVA possam utilizar os cookies, conforme abaixo:

   ```
   private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener() {
   @Override
   public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) {
   List<HttpCookie> cookies = cookiesUpdatedEvent.getHttpCookies();
   for(int i = 0; i < cookies.size(); i++)
   { HttpCookie c = cookies.get(i); // To set this cookie on to the cookie store //c.setValue("newValue"); //If you want to modify the value of the cookie URI myuri = URI.create(cookiesUpdatedEvent.getDomainString()); cookieManager.getCookieStore().add(myuri,c); }
   }
   }
   ```
