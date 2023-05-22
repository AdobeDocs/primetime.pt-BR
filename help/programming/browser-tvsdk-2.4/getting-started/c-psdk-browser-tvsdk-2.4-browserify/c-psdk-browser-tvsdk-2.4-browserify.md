---
description: Você pode criar um player compatível com Browserify usando arquivos JS fornecidos pelo TVSDK do Navegador.
title: Player compatível com Browserify
exl-id: 3e9751d8-7a7e-465b-8d46-d07e4ccb1f5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Visão geral {#browserify-compatible-player-overview}

Você pode criar um player compatível com Browserify usando arquivos JS fornecidos pelo TVSDK do Navegador.

O TVSDK do navegador fornece dois arquivos JS compatíveis com o Browserify. Um é para uso com o módulo AdobePSDK; isso é para o desenvolvimento de aplicativos sem a estrutura de interface do usuário. O outro é para uso com o módulo UI-Framework; retorna o namespace PTP usado para gravar aplicativos usando o UI-Framework.

Para começar a usar Browserify, execute os seguintes comandos de configuração para criar [!DNL final.js] (seu arquivo de pacote Browserify) dentro da variável [!DNL example] diretórios em [!DNL samples/browerify/reference] e [!DNL samples/browerify/ui-framework]:

1. Navegue até [!DNL samples/browserify/reference/build].
1. Execute os seguintes comandos:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Navegue até [!DNL samples/browserify/ui-framework/build].
1. Execute os mesmos comandos da Etapa 2.

Com essa configuração concluída, você pode continuar a criar aplicativos TVSDK compatíveis com o Browserify com base nos exemplos fornecidos com o TVSDK.
