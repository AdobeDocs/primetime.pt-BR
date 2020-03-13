---
description: Quando a decisão do anúncio Primetime encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ela avalia os anúncios de fallback para determinar o que retornar.
seo-description: Quando a decisão do anúncio Primetime encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ela avalia os anúncios de fallback para determinar o que retornar.
seo-title: Comportamento de fallback do anúncio para VAST e VMAP
title: Comportamento de fallback do anúncio para VAST e VMAP
uuid: 612416b9-d070-42e2-b68b-74ba52023345
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Comportamento de fallback do anúncio para VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando a decisão do anúncio Primetime encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ela avalia os anúncios de fallback para determinar o que retornar.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

No TVSDK, o único tipo de mídia válido é `application/x-mpegURL` (M3U8).

Quando há anúncios de fallback independentes, o plug-in de decisão do Primetime ad examina esses anúncios na seguinte ordem e retorna o primeiro anúncio com um tipo de mídia válido:

1. Se o reempacotamento estiver ativado, a primeira ocorrência de um anúncio com um tipo de mídia inválido será tratada como outros tipos de mídia inválidos.

   Se a reembalagem falhar, esse processo se aplica a ocorrências adicionais do anúncio.
1. Se o TVSDK não encontrar anúncios de fallback válidos, ele retornará o anúncio original com o tipo de mídia inválido.
1. Se um anúncio de fallback com um tipo MIME válido for retornado em vez do anúncio original, a decisão do anúncio Primetime envia o código de erro 403 para o URL de erro VAST, se disponível.
1. Se um anúncio de fallback for um invólucro e retornar vários anúncios, somente os anúncios com o tipo de mídia correto serão retornados.

>[!IMPORTANT]
>
>Esse comportamento é sempre ativado para anúncios em invólucros VAST. Para anúncios VAST em linha em um VMAP, o comportamento é desativado por padrão, mas seu aplicativo pode ativá-lo.