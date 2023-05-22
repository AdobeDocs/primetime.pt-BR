---
description: O TVSDK do navegador fornece ao aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.
title: Anúncios clicáveis
exl-id: 5fd8b38d-bde7-4d80-bfb0-3390c8f2665c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Visão geral {#clickable-ads-overview}

O TVSDK do navegador fornece ao aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.

Quando um usuário clica em um anúncio clicável, uma resposta típica de um aplicativo de vídeo é abrir uma nova janela do navegador e navegar até o URL associado ao anúncio. Para facilitar isso, o TVSDK do navegador aciona notificações de anúncios que seu aplicativo pode usar para gerenciar o processo de click-through.

No aplicativo, é possível fornecer ao usuário um controle para clicar (por exemplo, um botão) enquanto o anúncio clicável está sendo reproduzido. É necessário criar manipuladores para eventos acionados pelo TVSDK do navegador que estão associados ao anúncio (por exemplo, início do anúncio, anúncio clicado e anúncio concluído). Por fim, é necessário implementar os comportamentos específicos que seu aplicativo seguirá ao clicar em um anúncio do usuário (por exemplo, pausar ou não o anúncio, exibir o URL de click-through e assim por diante).

>[!NOTE]
>
>O reprodutor de referência incluído no TVSDK do navegador inclui uma solução de trabalho possível para processar anúncios de click-through.
