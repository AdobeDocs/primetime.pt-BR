---
description: O TVSDK do navegador fornece ao aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.
title: Anúncios clicáveis
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Visão geral {#clickable-ads-overview}

O TVSDK do navegador fornece ao aplicativo de vídeo as informações necessárias para responder ao clique de um usuário em um anúncio clicável.

Quando um usuário clica em um anúncio clicável, uma resposta típica de um aplicativo de vídeo é abrir uma nova janela do navegador e navegar até o URL associado ao anúncio. Para facilitar isso, o TVSDK do navegador aciona notificações e notificações que seu aplicativo pode usar para gerenciar o processo de click-through.

No seu aplicativo, você pode fornecer ao usuário um controle para clicar (por exemplo, um botão) enquanto o anúncio clicável está sendo reproduzido. Você precisa criar manipuladores para eventos acionados pelo Browser TVSDK associados ao anúncio (por exemplo, início do anúncio, anúncio clicado e anúncio concluído). Por fim, é necessário implementar os comportamentos específicos que o aplicativo seguirá ao clicar no anúncio de um usuário (por exemplo, pausar ou não o anúncio, exibir o URL de click-through e assim por diante).

>[!NOTE]
>
>O reprodutor de referência incluído no TVSDK do navegador inclui uma possível solução de trabalho para processar anúncios de click-through.