---
description: O suporte para o atributo withCredentials em XMLHttpRequests permite que as solicitações de compartilhamento de recursos de origem cruzada (CORS) incluam os cookies do domínio de destino para uma variedade de tipos de solicitação.
keywords: CORS;cross origin;resource sharing;cookies;withCredentials
seo-description: O suporte para o atributo withCredentials em XMLHttpRequests permite que as solicitações de compartilhamento de recursos de origem cruzada (CORS) incluam os cookies do domínio de destino para uma variedade de tipos de solicitação.
seo-title: Compartilhamento de recursos entre origens
title: Compartilhamento de recursos entre origens
uuid: e788b542-d4ac-48aa-91e2-1e88068cbba1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Compartilhamento de recursos entre origens {#cross-origin-resource-sharing}

O suporte para o atributo withCredentials em XMLHttpRequests permite que as solicitações de compartilhamento de recursos de origem cruzada (CORS) incluam os cookies do domínio de destino para uma variedade de tipos de solicitação.

Quando o cliente solicita um manifesto, segmento ou chave, o servidor pode definir um cookie que o cliente deve passar para as solicitações subsequentes. Para permitir a leitura e a gravação de cookies, o cliente deve definir o `withCredentials` atributo como `true` para solicitações entre origens.

Para ativar o `withCredentials` suporte para a maioria dos tipos de solicitações ao reproduzir um determinado recurso de mídia:

1. Crie o `CORSConfig` objeto.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Anexe o objeto `corsConfig` ao `NetworkConfiguration` objeto e defina `useCookieHeaderForAllRequests` como `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Definido `networkConfig` no `MediaPlayerItemConfig` objeto.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Passe `MediaPlayerItemConfig` para o `MediaPlayer.replaceCurrentResource` método.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>O sinalizador `useCookieHeaderForAllRequests` não afeta solicitações de licença. Para definir o `withCredentials` atributo como `true` para uma solicitação de licença, você deve definir o `withCredentials` atributo nos dados de proteção ou especificar uma chave de autorização na lista `httpRequestHeaders` de seus dados de proteção. Por exemplo:

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

O sinalizador não afeta uma solicitação de licença porque alguns servidores definem o `Access-Control-Allow-Origin` campo como curinga (&#39;*&#39;) em sua resposta. Mas, quando o sinalizador de credenciais está definido como `true`, o curinga não pode ser usado em `Access-Control-Allow-Origin`. Se você definir como `useCookieHeaderForAllRequests` `true` para todos os tipos de solicitações, poderá ver o seguinte erro para uma solicitação de licença:

Lembre-se das seguintes informações:

* Quando uma chamada com `withCredentials=true` falha, o TVSDK do navegador repete a chamada sem `withCredentials`.
* Quando uma chamada é feita com `networkConfiguration.useCookieHeaderForAllRequests=false`, as solicitações XHR são feitas sem o `withCredentials` atributo.