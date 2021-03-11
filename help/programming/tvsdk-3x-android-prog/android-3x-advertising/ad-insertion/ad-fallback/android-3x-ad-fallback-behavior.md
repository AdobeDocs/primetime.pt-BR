---
description: Quando o Primetime ad decisioning encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ele avalia os anúncios de fallback para determinar o que retornar.
title: Comportamento de fallback de anúncio para VAST e VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Comportamento de fallback de anúncio para VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando o Primetime ad decisioning encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ele avalia os anúncios de fallback para determinar o que retornar.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

No TVSDK, o único tipo de mídia válido é `application/x-mpegURL` (M3U8).

Quando há anúncios de fallback independentes, o plug-in de decisão do Primetime ad examina esses anúncios na seguinte ordem e retorna o primeiro anúncio com um tipo de mídia válido:

1. Se o reempacotamento estiver ativado, a primeira ocorrência de um anúncio com um tipo de mídia inválido será tratada como outros tipos de mídia inválidos.

   Se o reempacotamento falhar, esse processo se aplica às ocorrências adicionais do anúncio.
1. Se o TVSDK não encontrar anúncios de fallback válidos, ele retornará o anúncio original com o tipo de mídia inválido.
1. Se um anúncio de fallback com um tipo MIME válido for retornado em vez do anúncio original, o Primetime ad decisioning enviará o código de erro 403 para o URL de erro VAST, se disponível.
1. Se um anúncio de fallback for um wrapper e retornar vários anúncios, somente os anúncios com o tipo de mídia correto serão retornados.

>[!IMPORTANT]
>
>Esse comportamento é sempre ativado para anúncios em invólucros VAST. Para anúncios VAST em linha em um VMAP, o comportamento é desativado por padrão, mas o aplicativo pode habilitá-lo.