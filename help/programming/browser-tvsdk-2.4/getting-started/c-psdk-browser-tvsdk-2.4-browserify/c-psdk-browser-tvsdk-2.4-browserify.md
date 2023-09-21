---
description: Você pode criar um player compatível com Browserify usando arquivos JS fornecidos pelo TVSDK do Navegador.
title: Player compatível com Browserify
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
