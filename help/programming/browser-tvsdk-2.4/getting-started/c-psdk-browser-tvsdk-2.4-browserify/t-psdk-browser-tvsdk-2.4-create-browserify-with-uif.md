---
description: Use os arquivos de biblioteca do Browserify fornecidos pelo TVSDK do Navegador em seu aplicativo para criar um player compatível com Browserify usando a Estrutura de interface do usuário.
title: Criar um player compatível com Browserify usando a estrutura de interface do usuário
exl-id: cd72cae1-f67e-4192-9a7e-1c1492d88922
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Criar um player compatível com Browserify usando a estrutura de interface do usuário {#create-a-browserify-compatible-player-using-the-ui-framework}

Use os arquivos de biblioteca do Browserify fornecidos pelo TVSDK do Navegador em seu aplicativo para criar um player compatível com Browserify usando a Estrutura de interface do usuário.

Arquivos Browserify de exemplo incluídos no TVSDK:

* [!DNL [..]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/ui-framework/build/package.json]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.js]

Para criar um aplicativo compatível com Browserify usando a Estrutura de Interface de Usuário, você deve `require` os dois módulos Browserify (fornecidos pelo TVSDK do Navegador) no código do aplicativo:

1. Exigir módulos Browserify:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Continue o desenvolvimento conforme descrito em [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Agora você pode agrupar seus arquivos de aplicativo usando Browserify.
