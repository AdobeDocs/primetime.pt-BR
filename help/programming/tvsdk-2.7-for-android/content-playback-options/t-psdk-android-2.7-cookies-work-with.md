---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
seo-description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessão, acesso à porta e assim por diante.
seo-title: Trabalhar com cookies
title: Trabalhar com cookies
uuid: a3b966fd-1263-458d-8303-b4e898372ee1
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '258'
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

Crie um `cookieManager` e adicione seus cookies para os URIs ao cookieStore.

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

O evento MediaPlayerEvent.COOKIES_UPDATED é chamado quando os cookies C++ são atualizados. Este cookiesUpdatesEvent tem um método getCookieString() que retorna um valor de string para o cookie.

Um trecho de código de amostra está abaixo:

```
private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener()  
{ 
@Override 
public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) 
 { 
 String cookieStr = cookiesUpdatedEvent.getCookieString();  
 logger.i(LOG_TAG + "::MediaPlayer.CookiesUpdatedEventListener#onCookiesUpdated()", "cookieStr " + cookieStr);  
 }  
};
```

