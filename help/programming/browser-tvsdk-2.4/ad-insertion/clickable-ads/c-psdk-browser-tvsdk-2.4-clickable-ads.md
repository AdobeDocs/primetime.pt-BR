---
description: O TVSDK do navegador fornece ao seu aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.
seo-description: O TVSDK do navegador fornece ao seu aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.
seo-title: Anúncios clicáveis
title: Anúncios clicáveis
uuid: 493c3199-b5ba-4809-86eb-e80f10eb957b
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Visão geral {#clickable-ads-overview}

O TVSDK do navegador fornece ao seu aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.

Quando um usuário clica em um anúncio clicável, uma resposta típica de um aplicativo de vídeo é abrir uma nova janela do navegador e navegar até o URL associado ao anúncio. Para facilitar isso, o TVSDK do navegador aciona notificações de anúncio que seu aplicativo pode usar para gerenciar o processo de click-through.

No aplicativo, você pode fornecer ao usuário um controle para clicar (por exemplo, um botão) enquanto o anúncio clicável está sendo reproduzido. Você precisa criar manipuladores para eventos acionados pelo TVSDK do navegador que estão associados ao anúncio (por exemplo, start de anúncio, anúncio clicado e anúncio concluído). Por fim, é necessário implementar os comportamentos específicos que seu aplicativo seguirá ao clicar no anúncio do usuário (por exemplo, se deseja pausar o anúncio, exibir o URL de click-through e assim por diante).

>[!NOTE]
>
>O player de referência incluído no TVSDK do navegador inclui uma solução de trabalho possível para o processamento de anúncios de click-through.