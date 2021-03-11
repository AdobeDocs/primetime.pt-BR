---
description: Você pode usar o TVSDK para enviar dados arbitrários em cabeçalhos de cookies para gerenciamento de sessões, acesso à porta e assim por diante.
title: Trabalhar com cookies
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
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
>Quando o redirecionamento 302 é ativado, a solicitação de anúncio pode ser redirecionada para um domínio diferente do domínio ao qual o cookie pertence.

O TVSDK consulta esse `cookieManager` no tempo de execução, verifica se há cookies associados ao URL e usa esses cookies automaticamente.

O evento MediaPlayerEvent.COOKIES_UPDATED é chamado quando os cookies C++ são atualizados. Este cookiesUpdatedEvent tem um método getCookieString() que retorna um valor de string para o cookie.

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

