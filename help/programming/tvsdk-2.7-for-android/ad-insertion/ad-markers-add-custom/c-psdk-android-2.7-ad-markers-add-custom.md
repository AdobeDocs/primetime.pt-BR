---
description: Ao usar marcadores de anúncios personalizados, você pode marcar seções específicas do conteúdo principal como períodos de conteúdo relacionados a anúncios.
seo-description: Ao usar marcadores de anúncios personalizados, você pode marcar seções específicas do conteúdo principal como períodos de conteúdo relacionados a anúncios.
seo-title: Adicionar marcadores de anúncio personalizados
title: Adicionar marcadores de anúncio personalizados
uuid: 712da406-094a-49b2-b21d-4d5d73fff8cf
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# Visão geral {#add-custom-ad-markers-overview}

Ao usar marcadores de anúncios personalizados, você pode marcar seções específicas do conteúdo principal como períodos de conteúdo relacionados a anúncios.

Esse recurso é mais útil quando o conteúdo é gravado, por exemplo, a partir de um evento ao vivo, e o resultado da gravação é um fluxo HLS. A gravação contém o conteúdo principal e o conteúdo relacionado ao anúncio em um fluxo VOD (Video-on-demand) HLS. O processo de gravação não acompanha os segmentos relacionados ao anúncio, portanto, as informações relacionadas ao posicionamento dos anúncios no conteúdo principal são perdidas.

Você pode obter as informações relacionadas ao posicionamento dos períodos de conteúdo do anúncio de outras fontes fora da banda, como sistemas CMS externos. Você pode definir marcadores personalizados, através dos quais essas informações fora de banda podem ser passadas para o subsistema do gerenciador de linha do tempo. A intenção é marcar as seções de conteúdo que correspondem ao conteúdo relacionado ao anúncio especificado de forma que todos os eventos de reprodução específicos do anúncio sejam acionados da mesma maneira que se esses períodos de anúncio personalizados fossem explicitamente colocados na linha do tempo do player.

O rastreamento de anúncios não é manipulado internamente pelo TVSDK, como quando os anúncios são resolvidos pela decisão do anúncio da Adobe Primetime. No entanto, o TVSDK fornece as seguintes abstrações que definem a forma como o conteúdo relacionado a anúncios é representado na linha do tempo:

* O intervalo do anúncio

   Uma pausa de anúncio é uma lista ordenada de anúncios individuais consecutivos.
* Um anúncio individual

Os eventos de reprodução são acionados separadamente para pausas de anúncio e anúncios no start e no ponto final de cada anúncio.

O TVSDK despacha eventos de rastreamento de anúncio para seu aplicativo, para que você possa implementar sua própria lógica de rastreamento. Se definir marcadores de anúncio personalizados, você receberá os eventos `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete` e `onAdBreakComplete`.