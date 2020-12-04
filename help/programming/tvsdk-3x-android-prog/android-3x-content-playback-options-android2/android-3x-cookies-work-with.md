---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
seo-description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
seo-title: Trabalhar com cookies
title: Trabalhar com cookies
uuid: 618bc59a-032d-445e-a867-ed2bf260570d
translation-type: tm+mt
source-git-commit: 5ada8632a7a5e3cb5d795dc42110844244656095
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Trabalhar com cookies {#work-with-cookies}

Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.

Esta é uma amostra de solicitação ao servidor de chaves com alguma autenticação:

1. Seu cliente entra em seu site em um navegador e seu login mostra que este cliente tem permissão para visualização no conteúdo.
1. Com base no que é esperado pelo servidor de licenças, seu aplicativo gera um token de autenticação.

   Esse valor é passado para o TVSDK.
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
   >Quando o redirecionamento 302 estiver ativado, a solicitação de anúncio poderá ser redirecionada para um domínio diferente do domínio ao qual o cookie pertence.

   O TVSDK query esse `cookieManager` no tempo de execução, verifica se há cookies associados ao URL e usa esses cookies automaticamente.

   Se os cookies precisarem ser atualizados no aplicativo durante a reprodução, não use a API `networkConfiguration.setCookieHeaders`, pois a atualização ocorrerá no armazenamento de cookies JAVA.

   `networkConfiguration.setCookieHeaders` A API define os cookies como CookieStore C++ da TVSDK.

   Ao usar cookies JAVA e compartilhá-los entre o Aplicativo e o TVSDK, use o JAVA CookieStore para gerenciar os cookies exclusivamente.

   Antes de inicializar a reprodução, defina os cookies como CookieStore usando o Gerenciador de cookies, conforme mencionado acima.

   O cookie armazenado no CookieStore será automaticamente selecionado pelo TVSDK.

   Se um valor de cookie precisar ser atualizado posteriormente durante a reprodução, chame o mesmo método de adição de CookieStore com a mesma chave e um novo campo de valor.

   Também definido
   `networkConfiguration.setReadSetCookieHeader`(false) antes de chamar
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >Depois de definir &#39;setReadSetCookieHeader&#39; como falso, defina os cookies para as solicitações principais usando o gerenciador de cookies JAVA.

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
Essa API de retorno de chamada será acionada sempre que houver uma atualização em cookies C++ (cookies que vêm da resposta http). O aplicativo precisa ouvir esse retorno de chamada e pode atualizar seu JAVA CookieStore de acordo para que suas chamadas de rede em JAVA possam utilizar os cookies como abaixo:

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
