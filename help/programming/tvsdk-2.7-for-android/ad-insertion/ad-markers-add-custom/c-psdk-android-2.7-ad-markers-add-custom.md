---
description: Ao usar marcadores de anúncios personalizados, você pode marcar seções específicas do conteúdo principal como períodos de conteúdo relacionado a anúncios.
title: Adicionar marcadores de anúncio personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Visão geral {#add-custom-ad-markers-overview}

Ao usar marcadores de anúncios personalizados, você pode marcar seções específicas do conteúdo principal como períodos de conteúdo relacionado a anúncios.

Esse recurso é mais útil quando o conteúdo está sendo gravado, por exemplo, de um evento em tempo real, e o resultado da gravação é um fluxo de HLS. A gravação contém o conteúdo principal e o conteúdo relacionado à publicidade em um fluxo de vídeo sob demanda (VOD) do HLS. O processo de gravação não acompanha os segmentos relacionados a anúncios, portanto, as informações relacionadas ao posicionamento dos anúncios no conteúdo principal são perdidas.

Você pode obter as informações relacionadas ao posicionamento dos períodos de conteúdo do anúncio a partir de outras fontes fora de banda, como sistemas CMS externos. Você pode definir marcadores personalizados, através dos quais essas informações fora de banda podem ser passadas para o subsistema do gerenciador de linha do tempo. A intenção é marcar as seções de conteúdo que correspondem ao conteúdo relacionado a anúncios especificado, de forma que todos os eventos de reprodução específicos de anúncios sejam acionados da mesma maneira que esses períodos de anúncio personalizados eram explicitamente colocados na linha do tempo do reprodutor.

O rastreamento de anúncios não é manipulado internamente pelo TVSDK, como quando anúncios são resolvidos pelo Adobe Primetime ad decisioning. No entanto, o TVSDK fornece as seguintes abstrações que definem a forma como o conteúdo relacionado a anúncios é representado na linha do tempo:

* O ad break

   Um ad break é uma lista ordenada de anúncios individuais consecutivos.
* Um anúncio individual

Os eventos de reprodução são acionados separadamente para ad breaks e anúncios no ponto inicial e final de cada anúncio.

O TVSDK despacha eventos de rastreamento de anúncios para seu aplicativo, para que você possa implementar sua própria lógica de rastreamento. Se você definir marcadores de anúncio personalizados, receberá os eventos `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete` e `onAdBreakComplete`.