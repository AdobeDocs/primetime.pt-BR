---
description: O suporte para o atributo withCredentials em XMLHttpRequests permite que as solicitações de compartilhamento de recursos entre origens (CORS) incluam os cookies do domínio de destino para uma variedade de tipos de solicitação.
keywords: CORS;origem cruzada;compartilhamento de recursos;cookies;withCredentials
title: Compartilhamento de recursos entre origens
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Compartilhamento de recursos entre origens {#cross-origin-resource-sharing}

O suporte para o atributo withCredentials em XMLHttpRequests permite que as solicitações de compartilhamento de recursos entre origens (CORS) incluam os cookies do domínio de destino para uma variedade de tipos de solicitação.

Quando o cliente solicita um manifesto, segmento ou chave, o servidor pode definir um cookie que o cliente deve passar para as solicitações subsequentes. Para permitir a leitura e a gravação de cookies, o cliente deve definir a variável `withCredentials` atributo para `true` para solicitações entre origens.

Para habilitar `withCredentials` suporte para a maioria dos tipos de solicitações ao reproduzir um determinado recurso de mídia:

1. Crie o `CORSConfig` objeto.

   ```js
   var corsConfig = new AdobePSDK.CORSConfig();  
   corsConfig.enableEncryptionRequest = true; 
   ```

1. Anexe o `corsConfig` para o `NetworkConfiguration` object e set `useCookieHeaderForAllRequests` para `true`.

   ```js
   var networkConfig = new AdobePSDK.NetworkConfiguration();  
   networkConfig.CORSConfig = corsConfig; 
   networkConfiguration.useCookieHeaderForAllRequests= true;
   ```

1. Definir `networkConfig` no `MediaPlayerItemConfig` objeto.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig();  
   mediaPlayerItemConfig.networkConfiguration = networkConfig; 
   ```

1. Aprovado `MediaPlayerItemConfig` para o `MediaPlayer.replaceCurrentResource` método.

   ```js
   var player = new AdobePSDK.MediaPlayer(); 
   mediaResource = new AdobePSDK.MediaResource(url, AdobePSDK.MediaResourceType.HLS);  
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);  
   ```

>[!IMPORTANT]
>
>A variável `useCookieHeaderForAllRequests` O sinalizador não afeta solicitações de licença. Para definir a variável `withCredentials` atributo para `true` para uma solicitação de licença, você deve definir o `withCredentials` atributo nos dados de proteção ou especifique uma chave de autorização no `httpRequestHeaders` dos seus dados de proteção. Por exemplo:

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

O sinalizador não afeta uma solicitação de licença porque alguns servidores definem o `Access-Control-Allow-Origin` campo para curinga (&#39;&#42;&quot;) na sua resposta. Mas, quando o sinalizador de credenciais estiver definido como `true`, o curinga não pode ser usado no `Access-Control-Allow-Origin`. Se você definir `useCookieHeaderForAllRequests` para `true` para todos os tipos de solicitações, você pode ver o seguinte erro para uma solicitação de licença:

Lembre-se das seguintes informações:

* Quando uma chamada com `withCredentials=true` falha, o TVSDK do navegador tentará novamente a chamada sem `withCredentials`.
* Quando é feita uma chamada com `networkConfiguration.useCookieHeaderForAllRequests=false`, as solicitações XHR são feitas sem o `withCredentials` atributo.
