---
description: Você pode criar um player compatível com a Navegação usando arquivos JS fornecidos pelo TVSDK do navegador.
seo-description: Você pode criar um player compatível com a Navegação usando arquivos JS fornecidos pelo TVSDK do navegador.
seo-title: Player compatível com a navegação
title: Player compatível com a navegação
uuid: 1832c826-d5d0-41b0-852f-286c8e4fa0f3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Visão geral {#browserify-compatible-player-overview}

Você pode criar um player compatível com a Navegação usando arquivos JS fornecidos pelo TVSDK do navegador.

O TVSDK do navegador fornece dois arquivos JS compatíveis com o Browserify. Um é para uso com o módulo AdobePSDK; isso é para o desenvolvimento de aplicativos sem a estrutura da interface do usuário. O outro é para uso com o módulo UI-Framework; ele retorna a namespace PTP que você usa para gravar aplicativos usando a UI-Framework.

Para começar a usar o Browserify, execute os seguintes comandos de configuração para criar arquivos [!DNL final.js] (o arquivo do pacote Browserify) dentro dos diretórios [!DNL example] em [!DNL samples/browerify/reference] e [!DNL samples/browerify/ui-framework]:

1. Navegue até [!DNL samples/browserify/reference/build].
1. Execute os seguintes comandos:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Navegue até [!DNL samples/browserify/ui-framework/build].
1. Execute os mesmos comandos da Etapa 2.

Com essa configuração concluída, você pode continuar a criar aplicativos TVSDK compatíveis com o Browserify com base nas amostras fornecidas com o TVSDK.
