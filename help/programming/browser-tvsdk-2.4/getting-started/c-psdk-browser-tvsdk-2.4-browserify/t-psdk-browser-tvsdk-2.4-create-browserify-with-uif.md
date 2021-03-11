---
description: Use os arquivos da biblioteca Browserify fornecidos pelo Browser TVSDK no seu aplicativo para criar um player compatível com o Browserify usando a Estrutura da interface do usuário.
title: Criar um reprodutor compatível com o Browserify usando a Estrutura da Interface do Usuário
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Crie um reprodutor compatível com o Browserify usando a Estrutura da interface do usuário {#create-a-browserify-compatible-player-using-the-ui-framework}

Use os arquivos da biblioteca Browserify fornecidos pelo Browser TVSDK no seu aplicativo para criar um player compatível com o Browserify usando a Estrutura da interface do usuário.

Arquivos de pesquisa de exemplo incluídos no TVSDK:

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

Para criar um aplicativo compatível com o Browserify usando a Estrutura da interface do usuário, você deve `require` os dois módulos do Browserify (fornecidos pelo Browser TVSDK) no código do aplicativo:

1. Exigir módulos de Browserify:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Continue com o desenvolvimento conforme descrito em [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Agora é possível agrupar os arquivos do aplicativo usando o Browserify.
