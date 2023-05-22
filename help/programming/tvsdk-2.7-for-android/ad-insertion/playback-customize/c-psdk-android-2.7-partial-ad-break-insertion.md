---
title: Inserção parcial de Ad break
description: Inserção parcial de Ad break
copied-description: true
exl-id: bcd4b108-9b91-479e-8147-ec4d24862e37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Inserção parcial de Ad break {#partial-ad-break-insertion}

Você pode habilitar uma experiência tipo TV ao participar no meio de um anúncio, em transmissões ao vivo. O recurso Ad break parcial permite imitar uma experiência semelhante à de uma TV na qual, se o cliente iniciar um stream ao vivo dentro de um midroll, ele será iniciado dentro desse midroll. É como mudar para um canal de TV e os comerciais rodam perfeitamente.

Por exemplo, Se um usuário se juntar no meio de um ad break de 90 segundos (três anúncios de 30 segundos), 10 segundos no segundo anúncio (ou seja, a 40 segundos no ad break), o seguinte acontece:

* O segundo anúncio é reproduzido pelo tempo restante (20 segundos) seguido pelo terceiro anúncio.
* Os rastreadores de anúncios do anúncio parcialmente reproduzido (o segundo anúncio) não são acionados. Somente o rastreador do terceiro anúncio é acionado.

Esse comportamento não é ativado por padrão. Para habilitar este recurso, funcione no seu aplicativo, faça o seguinte:

1. Desative as pré-rolagens ao vivo, usando o método setEnableLivePreroll da classe AdvertisingMetadata.

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. Ative a preferência para Inserção ad-break parcial. Use o novo método setPartialAdBreakPref na interface do MediaPlayer para ativar esse recurso. Use o método getPartialAdBreakPref para encontrar o estado atual dessa preferência.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```
