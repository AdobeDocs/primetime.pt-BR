---
description: Use o arquivo da biblioteca Browserify fornecido pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação.
seo-description: Use o arquivo da biblioteca Browserify fornecido pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação.
seo-title: Crie um player compatível com a Navegação sem a Estrutura da interface do usuário
title: Crie um player compatível com a Navegação sem a Estrutura da interface do usuário
uuid: c4315bc8-c75d-4dd9-8680-946c1197be1e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Crie um player compatível com a Navegação sem a Estrutura da interface do usuário{#create-a-browserify-compatible-player-without-the-ui-framework}

Use o arquivo da biblioteca Browserify fornecido pelo TVSDK do navegador no seu aplicativo para criar um player compatível com a Navegação.

O tópico [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) lista o conjunto de bibliotecas TVSDK do navegador que você normalmente inclui ao criar um player de vídeo básico. Para fazer isso, basta adicionar `script` tags com `src` atributos apontando para as bibliotecas.

O processo é um pouco diferente para criar um player compatível com o Browserify. Para isso, use o `require` comando para incluir o [!DNL AdobePSDK.module.js] arquivo (fornecido pelo TVSDK do navegador) no aplicativo. Esse arquivo agrupa os arquivos básicos da biblioteca do player em sua ordem apropriada de dependência e retorna o `AdobePSDK` namespace que você usa para implementar os recursos do player.

O TVSDK do navegador fornece a seguinte amostra do aplicativo Browserify e dos arquivos de compilação no pacote de versão:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Para criar um player de vídeo compatível com a Navegação:

1. Exigir o arquivo de biblioteca compatível com Browserify que retorna o `AdobePSDK` namespace:

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
