---
description: Use o arquivo da biblioteca Browserify fornecido pelo Browser TVSDK no seu aplicativo para criar um player compatível com o Browserify.
title: Crie um reprodutor compatível com o Browserify sem a Estrutura da Interface do Usuário
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Crie um reprodutor compatível com o Browserify sem a Estrutura da Interface do Usuário{#create-a-browserify-compatible-player-without-the-ui-framework}

Use o arquivo da biblioteca Browserify fornecido pelo Browser TVSDK no seu aplicativo para criar um player compatível com o Browserify.

O tópico [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) lista o conjunto de bibliotecas TVSDK do navegador que você normalmente inclui ao criar um reprodutor de vídeo básico. Para fazer isso, basta adicionar `script` tags com atributos `src` apontando para as bibliotecas.

O processo é um pouco diferente para criar um reprodutor compatível com o Browserify. Para isso, use o comando `require` para incluir o arquivo [!DNL AdobePSDK.module.js] (fornecido pelo TVSDK do navegador) no aplicativo. Esse arquivo agrupa os arquivos básicos da biblioteca do reprodutor na ordem adequada de dependência e retorna o namespace `AdobePSDK` usado para implementar recursos no reprodutor.

O TVSDK do navegador fornece a seguinte amostra do aplicativo Browserify e dos arquivos de build no pacote de lançamento:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Para criar um reprodutor de vídeo compatível com o Browserify:

1. Requer o arquivo de biblioteca compatível com o Browserify que retorna o namespace `AdobePSDK`:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Crie seu reprodutor conforme descrito em [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   A Etapa 1 desta tarefa substitui a etapa nas instruções básicas do reprodutor, em que você cria as bibliotecas básicas individuais do reprodutor no arquivo do aplicativo.
Agora é possível agrupar os arquivos do aplicativo usando o Browserify.
