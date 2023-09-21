---
description: Quando o Primetime ad decisioning encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ele avalia os anúncios de fallback para determinar o que retornar.
title: Comportamento de fallback de anúncio para VAST e VMAP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Comportamento de fallback de anúncio para VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando o Primetime ad decisioning encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ele avalia os anúncios de fallback para determinar o que retornar.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

No TVSDK, o único tipo de mídia válido é `application/x-mpegURL` (M3U8) (em inglês).

Quando há anúncios de fallback independentes, o plug-in do Primetime ad decisioning examina esses anúncios na seguinte ordem e retorna o primeiro anúncio com um tipo de mídia válido:

1. Se o reempacotamento estiver ativado, a primeira ocorrência de um anúncio com um tipo de mídia inválido será tratada como outros tipos de mídia inválidos.

   Se o reempacotamento falhar, esse processo se aplica a ocorrências adicionais do anúncio.
1. Se o TVSDK não encontrar anúncios de fallback válidos, ele retornará o anúncio original com o tipo de mídia inválido.
1. Se um anúncio de fallback com um tipo MIME válido for retornado em vez do anúncio original, o Primetime ad decisioning enviará o código de erro 403 ao URL de erro VAST, se disponível.
1. Se um anúncio de fallback for um wrapper e retornar vários anúncios, somente os anúncios com o tipo de mídia correto serão retornados.

>[!IMPORTANT]
>
>Esse comportamento é sempre ativado para anúncios em invólucros VAST. Para anúncios VAST em linha em um VMAP, o comportamento é desativado por padrão, mas seu aplicativo pode ativá-lo.
