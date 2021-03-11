---
description: Você pode criar um reprodutor compatível com o Browserify usando arquivos JS fornecidos pelo Browser TVSDK.
title: Reprodutor compatível com o Browserify
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Visão geral {#browserify-compatible-player-overview}

Você pode criar um reprodutor compatível com o Browserify usando arquivos JS fornecidos pelo Browser TVSDK.

O TVSDK do navegador fornece dois arquivos JS compatíveis com o Browserify. Um é para uso com o módulo AdobePSDK; isso é para o desenvolvimento de aplicativos sem a estrutura da interface do usuário. O outro é para uso com o módulo de estrutura da interface do usuário; ele retorna o namespace PTP usado para escrever aplicativos usando a Estrutura da interface do usuário.

Para começar a usar o Browserify, execute os seguintes comandos de configuração para criar arquivos [!DNL final.js] (o arquivo do pacote Browserify) dentro dos diretórios [!DNL example] em [!DNL samples/browerify/reference] e [!DNL samples/browerify/ui-framework]:

1. Navegue até [!DNL samples/browserify/reference/build].
1. Execute os seguintes comandos:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Navegue até [!DNL samples/browserify/ui-framework/build].
1. Execute os mesmos comandos da Etapa 2.

Com essa configuração concluída, você pode continuar a criar aplicativos TVSDK compatíveis com o Browserify com base nas amostras fornecidas com o TVSDK.
