---
description: Use o arquivo da biblioteca Browserify fornecido pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação.
seo-description: Use o arquivo da biblioteca Browserify fornecido pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação.
seo-title: Crie um player compatível com a Navegação sem a Estrutura da interface do usuário
title: Crie um player compatível com a Navegação sem a Estrutura da interface do usuário
uuid: c4315bc8-c75d-4dd9-8680-946c1197be1e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Crie um player compatível com o Browserify sem a UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Use o arquivo da biblioteca Browserify fornecido pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação.

O tópico [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) lista o conjunto de bibliotecas TVSDK do navegador que você normalmente inclui ao criar um player de vídeo básico. Para fazer isso, basta adicionar `script` tags com atributos `src` apontando para as bibliotecas.

O processo é um pouco diferente para criar um player compatível com o Browserify. Para isso, use o comando `require` para incluir o arquivo [!DNL AdobePSDK.module.js] (fornecido pelo TVSDK do navegador) no aplicativo. Esse arquivo agrupa os arquivos básicos da biblioteca do player em sua ordem de dependência adequada e retorna a namespace `AdobePSDK` usada para implementar recursos para o player.

O TVSDK do navegador fornece a seguinte amostra do aplicativo Browserify e dos arquivos de compilação no pacote de versão:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Para criar um player de vídeo compatível com a Navegação:

1. Exigir o arquivo de biblioteca compatível com Browserify que retorna a namespace `AdobePSDK`:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Crie seu player conforme descrito em [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   A Etapa 1 desta tarefa substitui a etapa nas instruções básicas do player, na qual você cria as bibliotecas básicas individuais do player no arquivo do aplicativo.
Agora é possível agrupar os arquivos do aplicativo usando o Browserify.
