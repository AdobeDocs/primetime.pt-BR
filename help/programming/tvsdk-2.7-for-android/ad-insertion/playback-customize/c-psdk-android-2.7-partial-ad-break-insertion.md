---
description: nulo
seo-description: nulo
seo-title: Inserção parcial de quebra de anúncio
title: Inserção parcial de quebra de anúncio
uuid: cc071c89-f813-419e-a2b2-4f6a9fdccd6a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Inserção parcial de quebra de anúncio {#partial-ad-break-insertion}

Você pode habilitar uma experiência de TV de poder participar no meio de um anúncio, em fluxos ao vivo. O recurso de quebra parcial de anúncio permite que você imite uma experiência semelhante à TV em que, se o cliente start um fluxo ao vivo dentro de um midroll, ele será start dentro desse midroll. É como mudar para um canal de TV e os comerciais funcionam perfeitamente.

Por exemplo, se um usuário ingressar no meio de uma pausa de anúncio de 90 segundos (três anúncios de 30 segundos), 10 segundos após a segunda publicidade (ou seja, 40 segundos após a pausa), ocorrerá o seguinte:

* O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.
* Os rastreadores de anúncios para o anúncio parcialmente reproduzido (o segundo anúncio) não são acionados. Somente o rastreador do terceiro anúncio é disparado.

Esse comportamento não é ativado por padrão. Para ativar esse recurso no aplicativo, faça o seguinte:

1. Desative as pré-rolagens ao vivo, usando o método da classe AdvertisingMetadata setEnableLivePreroll.

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. Ative a preferência para Inserção parcial de quebra de anúncio. Use o novo método setPartialAdBreakPref na interface MediaPlayer para ativar esse recurso. Use o método getPartialAdBreakPref para encontrar o estado atual dessa preferência.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```

