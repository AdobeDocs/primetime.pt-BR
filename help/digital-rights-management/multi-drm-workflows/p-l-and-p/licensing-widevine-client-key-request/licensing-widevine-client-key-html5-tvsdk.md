---
description: O código pode solicitar uma chave por meio do DRMManager.
seo-description: O código pode solicitar uma chave por meio do DRMManager.
seo-title: Fluxo de trabalho de solicitação de chave em HTML5 TVSDK
title: Fluxo de trabalho de solicitação de chave em HTML5 TVSDK
uuid: a1f50eba-4301-49a1-b2e5-9add6687cff8
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Fluxo de trabalho de solicitação de chave em HTML5 TVSDK{#key-request-workflow-on-html-tvsdk}

O código pode solicitar uma chave por meio do DRMManager.

O TVSDK do navegador também expõe uma API setProtectionData por meio do objeto DRMManager:

```
[  /** 
   * This will only work for MSE. 
   * <p> Attach key system specific data to use for DRM 
license acquisition. </p> 
   * @param {Object} protectionData - an object containing property names corresponding to key system name strings 
   * (e.g. "org.w3.clearkey") and associated values being instances of 
   * MediaPlayer.vo.protection.ProtectionData. 
   * @returns {AdobePSDK.PSDKErrorCode} kECSuccess or one of the error codes. 
   * @function 
   * @memberof AdobePSDK.DRMManager# 
   */ 
   setProtectionData: function(protectionData) 
```

Seu código precisaria chamar essa API antes de iniciar a reprodução normal do conteúdo. MediaPlayer.vo.protection.ProtectionData está documentado aqui: [https://vm2.dashif.org/dash.js/docs/jsdocs/MediaPlayer.vo.protection.ProtectionData.html](https://vm2.dashif.org/dash.js/docs/jsdocs/MediaPlayer.vo.protection.ProtectionData.html)

Este é um exemplo de objeto de dados de proteção com URLs de servidor de licenças para PlayReady e Widevine.

```
var protectionData = { 
   "com.widevine.alpha": { 
                          "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/ 
                           ?ExpressPlayToken=AQAAABIDKA4AAABQuPPoebWWZZD2l3APRKkkagEDOXm 
                           CjgbhsqJTYeZ9KabkjCvSLvuXGHiVLymBnouGXDdCKpbz5IvB3jCZp9U05pys 
                           l9eavucsWXnA0tafbM-1SSJKXOa70kvxAJ_ybhdcmy7-6g" 
                          }, 
   "com.microsoft.playready": { 
                               "serverURL": "https://expressplay-licensing.axprod.net/ 
                                LicensingService.ashx?ExpressPlayToken=AQAAAw_ZXqcAAAB 
                                gHD1gnn_AMQJKfFCP3k9zbBw2srzBLryJVLXclnjhcSBCz4TBzrtfe 
                                gmSw1hAKdFHTNL-KVBGsI4ygBnfPRBUCvGsVOwpQ944fhq45W06ygJ 
                                roB2xOrM03tbkWcrthI7y_UQdHzufHjcBqKZm8QDoqKpxrxc" 
                               } 
   };
```

O TVSDK não fornece nenhuma API para forçar um sistema DRM específico, pois cada navegador suporta apenas um sistema DRM.
