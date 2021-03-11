---
title: Inserção parcial de ad break
description: Inserção parcial de ad break
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# Inserção parcial de ad break {#partial-ad-break-insertion}

Você pode habilitar uma experiência de TV de poder participar de um anúncio, em streams ao vivo. O recurso de Ad break parcial permite que você imite uma experiência semelhante a uma TV, onde, se o cliente iniciar um stream ao vivo dentro de um midroll, ele será iniciado dentro desse midroll. É semelhante a mudar para um canal de TV e os comerciais funcionam perfeitamente.

Por exemplo, se um usuário ingressar no meio de um ad break de 90 segundos (três anúncios de 30 segundos), 10 segundos no segundo anúncio (ou seja, 40 segundos após o ad break), o seguinte acontece:

* O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido do terceiro anúncio.
* Rastreadores de anúncios para o anúncio parcialmente reproduzido (o segundo anúncio) não são acionados. Somente o rastreador do terceiro anúncio é disparado.

Esse comportamento não é ativado por padrão. Para ativar este recurso no seu aplicativo, faça o seguinte:

ATIVE a preferência de Inserção parcial de quebra de anúncio. Use o novo método `setPartialAdBreakPref` na interface do MediaPlayer para ativar esse recurso. Use o método `getPartialAdBreakPref` para encontrar o estado atual dessa preferência.

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

O anúncio precedente, se disponível, é reproduzido e o conteúdo é reproduzido a partir do ponto ativo que emula a experiência da televisão ao vivo.
