---
description: As novas APIs a seguir permitem definir retornos de chamada de DRM.
title: Implementar retornos de chamada de DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Implementando retornos de chamada de DRM{#implementing-drm-callbacks}

As novas APIs a seguir permitem definir retornos de chamada de DRM.

<!--<a id="section_1090BFDB2C1D4EA4AAC9F9A6EC9DCD51"></a>-->

Você pode definir uma função de retorno de chamada (por exemplo, `parseContentIdCallback`) para analisar a ID de conteúdo e defini-la como `drmManager` usando a API `setParseContentIdCallback`.

```js
var arrayToString = function (array) { 
        var uint16array = new Uint16Array(array.buffer); 
        return String.fromCharCode.apply(null, uint16array); 
}, 
  
parseContentIdCallback = function (initData) { 
        var contentId = arrayToString(initData), 
            tokens = contentId?contentId.split('/'):[]; 
        if(tokens.length) { 
            return tokens[tokens.length-1]; 
        } else { 
            return ''; 
        } 
}; 
   
drmManager.setParseContentIdCallback(parseContentIdCallback);
```

<!--<a id="section_1E082B428EA74D9CA11C052158A83947"></a>-->

Você pode definir uma função de retorno de chamada (por exemplo, `onCertificateResponseCallback`) para processar uma resposta de certificado de texto e definir a função como `drmManager` usando a API `setCertificateResponseCallback`. Você pode definir `setCertificateResponseCallback` para substituir o comportamento padrão. Por exemplo, se você tiver um `certificateResponseType` que seja diferente de `ArrayBuffer`, poderá usar esse retorno de chamada para converter a resposta do certificado para o tipo `ArrayBuffer`.

```js
var base64DecodeUint8Array = function (input) { 
        var raw = window.atob(input); 
        var rawLength = raw.length; 
        var array = new Uint8Array(new ArrayBuffer(rawLength)); 
 
        for (var i = 0; i < rawLength; i++) 
            array[i] = raw.charCodeAt(i); 
 
        return array; 
    }, 
  
onCertificateResponseCallback = function (certificateResponse) { 
    if(certificateResponse) { 
        var certText = certificateResponse.trim(); 
        certText = certText.replace(/^"(.+(?="$))"$/, '$1'); 
        return base64DecodeUint8Array(certText); 
    } 
}; 
  
drmManager.setCertificateResponseCallback(onCertificateResponseCallback);
```

<!--<a id="section_4DCC1B3ABCED484EB5340A558C9A770A"></a>-->

Você pode definir funções de retorno de chamada para analisar a mensagem da licença e a resposta da licença e passá-las em uma chamada para `drmManager.acquireLicense`. `onLicenseResponseCallback` é um novo parâmetro na  `acquireLicense` API.

```js
var base64EncodeUint8Array = function (input) { 
        var keyStr = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/="; 
        var output = ""; 
        var chr1, chr2, chr3, enc1, enc2, enc3, enc4; 
        var i = 0; 
        while (i < input.length) { 
            chr1 = input[i++]; 
            chr2 = i < input.length ? input[i++] : Number.NaN; // Not sure if the index 
            chr3 = i < input.length ? input[i++] : Number.NaN; // checks are needed here 
  
            enc1 = chr1 >> 2; 
            enc2 = ((chr1 & 3) << 4) | (chr2 >> 4); 
            enc3 = ((chr2 & 15) << 2) | (chr3 >> 6); 
            enc4 = chr3 & 63; 
  
            if (isNaN(chr2)) { 
                enc3 = enc4 = 64; 
            } else if (isNaN(chr3)) { 
                enc4 = 64; 
            } 
            output += keyStr.charAt(enc1) + keyStr.charAt(enc2) + 
                keyStr.charAt(enc3) + keyStr.charAt(enc4); 
        } 
        return output; 
    }, 
  
    base64DecodeUint8Array = function (input) { 
        var raw = window.atob(input); 
        var rawLength = raw.length; 
        var array = new Uint8Array(new ArrayBuffer(rawLength)); 
  
        for (var i = 0; i < rawLength; i++) 
            array[i] = raw.charCodeAt(i); 
  
        return array; 
    }, 
  
    onLicenseMessageCallback = function (drmLicenseRequest) { 
        var licenseMessage = drmLicenseRequest.licenseMessage, 
            base64Message = base64EncodeUint8Array(licenseMessage); 
        return base64Message; 
    }, 
  
    onLicenseResponseCallback = function (serverResponse) { 
        var keyText = serverResponse.licenseResponse.trim(); 
        keyText = keyText.replace(/^"(.+(?="$))"$/, '$1'); 
        return base64DecodeUint8Array(keyText); 
    };

drmManager.acquireLicense(drmMetadata, null, acquireLicenseListener, onLicenseMessageCallback, onLicenseResponseCallback);
```

Nos dados de Proteção, o novo campo **[!UICONTROL certificateResponseType]** é usado para definir o tipo de resposta do certificado. Este é um exemplo de dados de proteção:

```js
{ 
     "com.apple.fps.1_0": { 
         "serverURL": "https://fairplay.license.istreamplanet.com/api/license/9d3ed760-3ba9-4042-b4a4-07e0d8069200", 
         "certificateURL":"https://fairplay-stage.license.istreamplanet.com/api/AppCert/9d3ed760-3ba9-4042-b4a4-07e0d8069200", 
         "licenseResponseType": "text", 
         "certificateResponseType": "text", 
         "httpRequestHeaders": { 
            "Content-type": "application/x-www-form-urlencoded" 
         } 
     } 
}
```

O uso do campo `certificateResponseType` é opcional. Se não for usado, o valor será considerado `ArrayBuffer`.
