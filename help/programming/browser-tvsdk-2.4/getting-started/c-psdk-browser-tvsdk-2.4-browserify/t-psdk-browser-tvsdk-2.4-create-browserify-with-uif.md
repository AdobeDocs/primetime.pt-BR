---
description: Use os arquivos da biblioteca Browserify fornecidos pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação usando a UI-Framework.
seo-description: Use os arquivos da biblioteca Browserify fornecidos pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação usando a UI-Framework.
seo-title: Criar um player compatível com a Navegação usando a Estrutura da interface do usuário
title: Criar um player compatível com a Navegação usando a Estrutura da interface do usuário
uuid: 544fd872-5ca1-417d-8aab-69613caada0e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Criar um player compatível com a Navegação usando a Estrutura da interface do usuário {#create-a-browserify-compatible-player-using-the-ui-framework}

Use os arquivos da biblioteca Browserify fornecidos pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação usando a UI-Framework.

Arquivos de pesquisa de amostra incluídos no TVSDK:

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

Para criar um aplicativo compatível com o Browserify usando a UI-Framework, você deve usar `require` os dois módulos do Browserify (fornecidos pelo TVSDK do navegador) no código do aplicativo:

1. Exigir módulos Browserify:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Prossiga com o desenvolvimento conforme descrito em [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Agora é possível agrupar os arquivos do aplicativo usando o Browserify.
