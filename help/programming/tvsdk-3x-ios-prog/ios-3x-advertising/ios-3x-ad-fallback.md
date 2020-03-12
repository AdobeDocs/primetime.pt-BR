---
description: Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
seo-description: Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
seo-title: Anúncio de fallback para anúncios VAST e VMAP
title: Anúncio de fallback para anúncios VAST e VMAP
uuid: ca65f349-012d-49e3-8c23-fd041c5362ee
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Anúncio de fallback para anúncios VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

A especificação VAST/Digital Video Multiple Ad Playlist (VMAP) declara que para anúncios nos quais o fallback VAST está ativado, anúncios vazios acionam automaticamente o uso de anúncios de fallback. Quando um anúncio VAST está vazio, o TVSDK procura uma substituição válida do tipo de mídia HLS entre os anúncios de fallback. Quando um anúncio VAST em um invólucro tem um tipo de mídia inválido, o TVSDK trata esse anúncio como vazio. Você pode configurar se o TVSDK deve fazer o mesmo para anúncios em linha em um VMAP. Para obter mais informações sobre o `fallbackOnNoAd` recurso VAST, consulte Modelo de disponibilização de vídeo [digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definir comportamento de anúncio de fallback para anúncios em linha VMAP {#section_D90BB3C6E539472EABF000C0F616DBE2}

Você pode ativar o fallback quando um anúncio em linha VMAP contiver um tipo de mídia inválido.

1. Defina `FallbackOnInvalidCreativeEnabled` para que `YES` o VMAP volte quando o tipo de mídia para um anúncio linear/inline for inválido para HLS.

   >[!NOTE]
   >
   >O valor padrão é NO. Se um anúncio linear falhar porque tem um tipo de mídia inválido, ou porque o anúncio não pode ser reempacotado, esse sinalizador permite que a decisão do anúncio Primetime siga o mesmo comportamento de fallback que se o anúncio fosse um invólucro VAST vazio.

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## Comportamento de fallback do anúncio para VAST e VMAP {#section_5B6716CC49CC4C40964CFE9F122C57A6}

Quando a decisão do anúncio Primetime encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ela avalia os anúncios de fallback para determinar o que retornar.

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