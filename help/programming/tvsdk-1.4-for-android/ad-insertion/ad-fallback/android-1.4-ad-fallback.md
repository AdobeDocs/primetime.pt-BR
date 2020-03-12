---
description: Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
seo-description: Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
seo-title: Anúncio de fallback para anúncios VAST e VMAP
title: Anúncio de fallback para anúncios VAST e VMAP
uuid: 5469cd22-7121-49f0-8833-2a525c7ef7d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Anúncio de fallback para anúncios VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

A especificação VAST/Digital Video Multiple Ad Playlist (VMAP) declara que para anúncios nos quais o fallback VAST está ativado, anúncios vazios acionam automaticamente o uso de anúncios de fallback. Quando um anúncio VAST está vazio, o TVSDK procura uma substituição válida do tipo de mídia HLS entre os anúncios de fallback. Quando um anúncio VAST em um invólucro tem um tipo de mídia inválido, o TVSDK trata esse anúncio como vazio. Você pode configurar se o TVSDK deve fazer o mesmo para anúncios em linha em um VMAP. Para obter mais informações sobre o `fallbackOnNoAd` recurso VAST, consulte Modelo de disponibilização de vídeo [digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definir comportamento de anúncio de fallback para anúncios em linha VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Você pode ativar o fallback quando um anúncio em linha VMAP contiver um tipo de mídia inválido.

1. Defina `setFallbackOnInvalidCreativeEnabled` para que `true` o VMAP volte quando o tipo de mídia para um anúncio linear/inline for inválido para HLS.

   O valor padrão é false. Se um anúncio linear falhar porque tem um tipo de mídia inválido, ou porque o anúncio não pode ser reempacotado, esse sinalizador permite que a decisão do anúncio Primetime siga o mesmo comportamento de fallback que se o anúncio fosse um invólucro VAST vazio.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

## Comportamento de fallback do anúncio para VAST e VMAP {#ad-fallback-behavior-for-vast-and-vmap}

Quando a decisão do anúncio Primetime encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ela avalia os anúncios de fallback para determinar o que retornar.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

No TVSDK, o único tipo de mídia válido é `application/x-mpegURL` (M3U8).

Quando há anúncios de fallback independentes, o plug-in de decisão do anúncio Primetime examina esses anúncios na seguinte ordem e retorna o primeiro anúncio com um tipo de mídia válido:

1. Se o reempacotamento estiver ativado, a primeira ocorrência de um anúncio com um tipo de mídia inválido será tratada como outros tipos de mídia inválidos.

   Se a reembalagem falhar, esse processo se aplica a ocorrências adicionais do anúncio.
1. Se o TVSDK não encontrar anúncios de fallback válidos, ele retornará o anúncio original com o tipo de mídia inválido.
1. Se um anúncio de fallback com um tipo MIME válido for retornado em vez do anúncio original, a decisão do anúncio Primetime envia o código de erro 403 para o URL de erro VAST, se disponível.
1. Se um anúncio de fallback for um invólucro e retornar vários anúncios, somente os anúncios com o tipo de mídia correto serão retornados.

>[!IMPORTANT]
>
>Esse comportamento é sempre ativado para anúncios em invólucros VAST. Para anúncios VAST em linha em um VMAP, o comportamento é desativado por padrão, mas seu aplicativo pode ativá-lo.