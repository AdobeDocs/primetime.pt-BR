---
description: Ao usar marcadores de anúncios personalizados, é possível marcar seções específicas do conteúdo principal como períodos de conteúdo relacionados a anúncios.
title: Adicionar marcadores de publicidade personalizados
exl-id: 310b2b81-873f-4b37-b18d-d586e6408978
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Visão geral {#add-custom-ad-markers-overview}

Ao usar marcadores de anúncios personalizados, é possível marcar seções específicas do conteúdo principal como períodos de conteúdo relacionados a anúncios.

Esse recurso é mais útil quando o conteúdo está sendo gravado, por exemplo, de um evento ao vivo, e o resultado da gravação é um fluxo HLS. A gravação contém o conteúdo principal e o conteúdo relacionado à publicidade em um fluxo de vídeo sob demanda (VOD) do HLS. O processo de gravação não rastreia os segmentos relacionados ao anúncio, portanto, as informações relacionadas ao posicionamento dos anúncios no conteúdo principal são perdidas.

Você pode obter as informações relacionadas ao posicionamento dos períodos de conteúdo de anúncio de outras fontes fora da banda, como sistemas CMS externos. Você pode definir marcadores personalizados, através dos quais essas informações fora de banda podem ser passadas para o subsistema do gerenciador de linha do tempo. A intenção é marcar as seções de conteúdo que correspondem ao conteúdo relacionado ao anúncio especificado, de modo que todos os eventos de reprodução específicos do anúncio sejam acionados da mesma maneira que se esses períodos de anúncio personalizados fossem explicitamente colocados na linha do tempo do reprodutor.

O rastreamento de anúncios não é feito internamente pelo TVSDK, por exemplo, quando os anúncios são resolvidos pelo Adobe Primetime ad decisioning. No entanto, o TVSDK fornece as seguintes abstrações que definem a forma como o conteúdo relacionado a anúncios é representado na linha do tempo:

* O ad break

   Um ad break é uma lista ordenada de anúncios consecutivos individuais.
* Um anúncio individual

Os eventos de reprodução são acionados separadamente para ad breaks e anúncios no ponto inicial e final de cada anúncio.

O TVSDK despacha eventos de rastreamento de anúncios para o aplicativo, para que você possa implementar sua própria lógica de rastreamento. Se você definir marcadores de anúncios personalizados, receberá a `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete`, e `onAdBreakComplete` eventos.
