---
description: Use o arquivo de biblioteca Browserify fornecido pelo TVSDK do Navegador em seu aplicativo para criar um player compatível com Browserify.
title: Criar um player compatível com Browserify sem a estrutura de interface do usuário
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Criar um player compatível com Browserify sem a estrutura de interface do usuário{#create-a-browserify-compatible-player-without-the-ui-framework}

Use o arquivo de biblioteca Browserify fornecido pelo TVSDK do Navegador em seu aplicativo para criar um player compatível com Browserify.

O tópico [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) lista o conjunto de bibliotecas TVSDK do navegador que você normalmente inclui ao criar um player de vídeo básico. Para fazer isso, basta adicionar `script` tags com `src` atributos que apontam para as bibliotecas.

O processo é um pouco diferente para criar um player compatível com Browserify. Para isso, use o `require` comando para incluir o [!DNL AdobePSDK.module.js] (fornecido pelo TVSDK do navegador) no aplicativo. Esse arquivo agrupa os arquivos básicos da biblioteca do player em sua ordem adequada de dependência e retorna a variável `AdobePSDK` namespace que você usa para implementar recursos para seu reprodutor.

O TVSDK do navegador fornece a seguinte amostra do aplicativo Browserify e dos arquivos de build no pacote de versão:

* [!DNL [..]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/reference/build/package.json]
* [!DNL [..]/samples/browserify/reference/examples/sample.html]
* [!DNL [..]/samples/browserify/reference/examples/sample.js]

Para criar um player de vídeo compatível com Browserify:

1. Exigir o arquivo de biblioteca compatível com Browserify que retorna o `AdobePSDK` namespace:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Crie seu reprodutor conforme descrito em [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   A etapa 1 nesta tarefa substitui a etapa nas instruções básicas do player nas quais você origina as bibliotecas básicas individuais do player no arquivo de aplicativo.
Agora você pode agrupar seus arquivos de aplicativo usando Browserify.
