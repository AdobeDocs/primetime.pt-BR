---
description: Para anúncios VAST (Modelo de veiculação de anúncio de vídeo digital) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
title: Reversão de anúncio para anúncios VAST e VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Ad fallback para anúncios VAST e VMAP {#ad-fallback-for-vast-and-vmap-ads}

Para anúncios VAST (Modelo de veiculação de anúncio de vídeo digital) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

A especificação VAST/Digital Video Multiple Ad Playlist (VMAP) declara que, para anúncios em que o fallback VAST é ativado, anúncios vazios acionam automaticamente o uso de anúncios de fallback. Quando um anúncio VAST está vazio, o TVSDK procura uma substituição válida do tipo de mídia HLS entre os anúncios de fallback. Quando um anúncio VAST em um invólucro tem um tipo de mídia inválido, o TVSDK trata esse anúncio como vazio. Você pode configurar se o TVSDK deve fazer o mesmo para anúncios em linha em um VMAP. Para obter mais informações sobre o recurso VAST `fallbackOnNoAd`, consulte [Modelo de veiculação de anúncio de vídeo digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definir o comportamento do anúncio de fallback para anúncios em linha do VMAP {#section_D90BB3C6E539472EABF000C0F616DBE2}

Você pode ativar o fallback quando um anúncio em linha do VMAP contiver um tipo de mídia inválido.

1. Defina `FallbackOnInvalidCreativeEnabled` como `YES` para que o VMAP retorne quando o tipo de mídia para um anúncio linear/em linha for inválido para HLS.

   >[!NOTE]
   >
   >O valor padrão é NO. Se um anúncio linear falhar porque tem um tipo de mídia inválido ou porque o anúncio não pode ser reempacotado, esse sinalizador permite que o Primetime ad decisioning siga o mesmo comportamento de fallback que se o anúncio fosse um invólucro VAST vazio.

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## Comportamento de fallback de anúncio para VAST e VMAP {#section_5B6716CC49CC4C40964CFE9F122C57A6}

Quando o Primetime ad decisioning encontra um anúncio VAST (criativo) vazio ou com um tipo de mídia inválido para HLS, ele avalia os anúncios de fallback para determinar o que retornar.

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