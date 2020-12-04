---
description: O suporte para o atributo withCredentials em XMLHttpRequests permite que as solicitações de compartilhamento de recursos (CORS) entre origens incluam os cookies do domínio do público alvo para uma variedade de tipos de solicitação.
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: O suporte para o atributo withCredentials em XMLHttpRequests permite que as solicitações de compartilhamento de recursos (CORS) entre origens incluam os cookies do domínio do público alvo para uma variedade de tipos de solicitação.
seo-title: Compartilhamento de recursos entre origens
title: Compartilhamento de recursos entre origens
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Compartilhamento de recursos entre origens {#cross-origin-resource-sharing}

O suporte para o atributo withCredentials em XMLHttpRequests permite que as solicitações de compartilhamento de recursos (CORS) entre origens incluam os cookies do domínio do público alvo para uma variedade de tipos de solicitação.

Quando o cliente solicita um manifesto, segmento ou chave, o servidor pode definir um cookie que o cliente deve passar para as solicitações subsequentes. Para permitir a leitura e a gravação de cookies, o cliente deve definir o atributo `withCredentials` como `true` para solicitações de origem cruzada.

Para habilitar o suporte `withCredentials` para a maioria dos tipos de solicitações ao reproduzir um determinado recurso de mídia:

1. Crie o objeto `CORSConfig`.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Anexe `corsConfig` ao objeto `NetworkConfiguration` e defina `useCookieHeaderForAllRequests` como `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Defina `networkConfig` no objeto `MediaPlayerItemConfig`.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Passe `MediaPlayerItemConfig` para o método `MediaPlayer.replaceCurrentResource`.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>O sinalizador `useCookieHeaderForAllRequests` não afeta as solicitações de licença. Para definir o atributo `withCredentials` como `true` para uma solicitação de licença, você deve definir o atributo `withCredentials` nos dados de proteção ou especificar uma chave de autorização em `httpRequestHeaders` dos dados de proteção. Por exemplo:

```
# Example 1 
{ 
    "com.widevine.alpha": {  
        "withCredentials":true,  
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i]" } 
} 
 
# Example 2 
{ 
    "com.widevine.alpha": { 
        "httpRequestHeaders": {  
            "authorization": "true"  
            }, 
        "serverURL":  
          "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=[YOUR_TOKEN</i>]" }
        } 
}
```

O sinalizador não afeta uma solicitação de licença porque alguns servidores definem o campo `Access-Control-Allow-Origin` como curinga (&#39;*&#39;) em sua resposta. Mas, quando o sinalizador de credenciais está definido como `true`, o curinga não pode ser usado em `Access-Control-Allow-Origin`. Se você definir `useCookieHeaderForAllRequests` como `true` para todos os tipos de solicitações, poderá ver o seguinte erro para uma solicitação de licença:

Lembre-se das seguintes informações:

* Quando uma chamada com `withCredentials=true` falha, o TVSDK do navegador tentativas a chamada sem `withCredentials`.
* Quando uma chamada é feita com `networkConfiguration.useCookieHeaderForAllRequests=false`, as solicitações XHR são feitas sem o atributo `withCredentials`.