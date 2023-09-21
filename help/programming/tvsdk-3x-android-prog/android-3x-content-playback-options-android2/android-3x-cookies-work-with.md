---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
title: Trabalhar com cookies
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Trabalhar com cookies {#work-with-cookies}

Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.

Este é um exemplo de solicitação para o servidor de chaves com alguma autenticação:

1. O cliente faz logon no site em um navegador e o logon mostra que ele tem permissão para visualizar o conteúdo.
1. Com base no que é esperado pelo servidor de licenças, seu aplicativo gera um token de autenticação.

   Esse valor é passado para o TVSDK.
1. O TVSDK define esse valor no cabeçalho do cookie.
1. Quando o TVSDK faz uma solicitação ao servidor de chaves para obter uma chave para descriptografar o conteúdo, a solicitação contém o valor de autenticação no cabeçalho do cookie.

   O servidor de chaves sabe que a solicitação é válida.

Para trabalhar com cookies:

1. Criar um `cookieManager` e adicione seus cookies para os URIs ao cookieStore.

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
   >Quando o redirecionamento 302 está ativado, a solicitação de anúncio pode ser redirecionada para um domínio diferente do domínio ao qual o cookie pertence.

   O TVSDK consulta isso `cookieManager` no tempo de execução, o verifica se há cookies associados ao URL e usa esses cookies automaticamente.

   Se for necessário atualizar os cookies no aplicativo durante a reprodução, não use `networkConfiguration.setCookieHeaders` API, pois a atualização ocorrerá no armazenamento de cookies JAVA.

   `networkConfiguration.setCookieHeaders` A API define os cookies para o C++ CookieStore do TVSDK.

   Ao usar cookies JAVA e compartilhá-los entre o Application e o TVSDK, use o JAVA CookieStore para gerenciar os cookies exclusivamente.

   Antes de inicializar a reprodução, defina os cookies para CookieStore usando o Gerenciador de cookies conforme descrito acima.

   O cookie armazenado no CookieStore será selecionado automaticamente pelo TVSDK.

   Se um valor de cookie precisar ser atualizado posteriormente durante a reprodução, chame o mesmo método add de CookieStore com a mesma chave e um novo campo de valor.

   Também definir
   `networkConfiguration.setReadSetCookieHeader`(false) antes de chamar
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >Depois de definir &quot;setReadSetCookieHeader&quot; como falso, defina os cookies para as solicitações de chave usando o gerenciador de cookies JAVA.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Essa API de retorno de chamada será acionada sempre que houver uma atualização nos cookies C++ (cookies provenientes da resposta http). O aplicativo precisa ouvir esse retorno de chamada e pode atualizar o JAVA CookieStore de acordo, para que suas chamadas de rede no JAVA possam utilizar os cookies conforme abaixo:

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
