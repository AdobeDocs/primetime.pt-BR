---
description: O TVSDK do navegador fornece uma interface DRM que você pode usar para reproduzir conteúdo protegido por diferentes soluções DRM, incluindo o FairPlay, PlayReady e Widevine.
seo-description: O TVSDK do navegador fornece uma interface DRM que você pode usar para reproduzir conteúdo protegido por diferentes soluções DRM, incluindo o FairPlay, PlayReady e Widevine.
seo-title: Visão geral da interface do DRM
title: Visão geral da interface do DRM
uuid: b553ebad-8310-4517-8d97-ef8a1c5f4340
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Visão geral da interface do DRM{#drm-interface-overview}

O TVSDK do navegador fornece uma interface DRM que você pode usar para reproduzir conteúdo protegido por diferentes soluções DRM, incluindo o FairPlay, PlayReady e Widevine.

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>O suporte a DRM está disponível para streams MPEG-Dash protegidos com sistemas DRM Microsoft PlayReady (no Internet Explorer no Windows 8.1 e Edge) e Widevine (no Google Chrome). O suporte a DRM está disponível para fluxos HLS no Safari que são protegidos com o FairPlay.

A interface principal do fluxo de trabalho do DRM é a `DRMManager`. Uma referência à `DRMManager` instância pode ser obtida por meio da instância MediaPlayer:

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

Este é um fluxo de trabalho de alto nível para reprodução de conteúdo protegido por DRM:

1. Para anexar os dados específicos do sistema DRM que serão usados pelo TVSDK do navegador no processo de aquisição de licença para um fluxo protegido, faça a seguinte chamada antes de chamar `mediaPlayer.replaceCurrentResource`:

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
          "serverURL": { 
             "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
             "license-request": "https://example.com:8096/flashaccess/req", 
             "license-release": "https://example.com:8096/flashaccess/req" 
          }, 
          "httpRequestHeaders": { 
          } 
       } 
   }; 
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. Se for esperado que o mesmo conteúdo funcione com diferentes sistemas DRM em navegadores diferentes, os dados de proteção poderão ser especificados para vários sistemas DRM.

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
           "serverURL": { 
               "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
               "license-request": "https://example.com:8096/flashaccess/req", 
               "license-release": "https://example.com:8096/flashaccess/req" 
           }, 
           "httpRequestHeaders": { 
           } 
       }, 
       "com.widevine.alpha": { 
           "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "dt-custom-data": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.microsoft.playready": { 
           "serverURL": "https://pr.test.expressplay.com/playready/RightsManager.asmx?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.apple.fps.1_0": { 
           "serverURL": "https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<token value>", 
           "certificateURL": "Path_To_certificate.cer", 
           "licenseResponseType": "arraybuffer", 
           "httpRequestHeaders": { 
               "Content-type": "application/octet-stream" 
           } 
       }, 
       "org.w3.clearkey": { 
           "clearkeys": { 
               "H3JbV93QV3mPNBKQON2UtQ": "ClKhDPHMtCouEx1vLGsJsA", 
               "IAAAACAAIAAgACAAAAAAAg": "5t1CjnbMFURBou087OSj2w" 
           } 
       } 
   }; 
   
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. Quando os dados de proteção não estão definidos, as informações necessárias, como o URL da licença, são recuperadas da caixa PSSH para sistemas DRM, onde aplicável.

   >[!TIP]
   >
   >A especificação de dados de proteção substitui o URL da licença especificado na caixa PSSH.

1. Por padrão, o tipo de sessão da licença DRM é temporário, o que significa que a licença não é armazenada depois que a sessão é fechada.

   Você pode especificar um tipo de sessão usando uma API em `DRMManager`.  Para compatibilidade com versões anteriores, os tipos de sessão incluem `temporary`, `persistent-license`, `persistent-usage-record`e `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. Quando o `sessionType` usado é `persistent-license` ou `persistent`, a licença DRM pode ser devolvida chamando-se `DRMManager.returnLicense`.

   ```js
   var onLicenseReturnFunc = function () { 
       console.log("DRM: License Return Complete "); 
   }, 
   
   onLicenseReturnErrorFunc = function (major, minor, errorString/*, errorServerUrl*/) { 
      console.log("DRM: License Return Error: " + errorString); 
   }, 
   
   drmManager = mediaPlayer.drmManager; 
   
   if (drmManager) { 
       var returnLicenseListener = new  
           AdobePSDK.DRMReturnLicenseListener(onLicenseReturnFunc, onLicenseReturnErrorFunc); 
       drmManager.returnLicense(null, null, null, false, returnLicenseListener, drmLicense.session); 
   }
   ```

