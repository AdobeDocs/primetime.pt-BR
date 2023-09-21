---
description: O TVSDK do navegador fornece ao aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.
title: Anúncios clicáveis
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Visão geral {#clickable-ads-overview}

O TVSDK do navegador fornece ao aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.

Quando um usuário clica em um anúncio clicável, uma resposta típica de um aplicativo de vídeo é abrir uma nova janela do navegador e navegar até o URL associado ao anúncio. Para facilitar isso, o TVSDK do navegador dispara notificações de anúncios que seu aplicativo pode usar para gerenciar o processo de click-through.

No aplicativo, é possível fornecer ao usuário um controle para clicar (por exemplo, um botão) enquanto o anúncio clicável está sendo reproduzido. É necessário criar manipuladores para eventos acionados pelo TVSDK do navegador que estão associados ao anúncio (por exemplo, início do anúncio, anúncio clicado e anúncio concluído). Por fim, é necessário implementar os comportamentos específicos que seu aplicativo seguirá ao clicar em um anúncio do usuário (por exemplo, pausar ou não o anúncio, exibir o URL de click-through e assim por diante).

>[!NOTE]
>
>O reprodutor de referência incluído no TVSDK do navegador inclui uma solução de trabalho possível para processar anúncios de click-through.
