---
description: nulo
seo-description: nulo
seo-title: Inserção parcial de quebra de anúncio
title: Inserção parcial de quebra de anúncio
uuid: a81295b8-77fe-4475-a472-080ee7804d7a
translation-type: tm+mt
source-git-commit: fe9d7d1b2b23a70eb4e212de3d9bda47fc11d8f1

---


# Inserção parcial de quebra de anúncio {#partial-ad-break-insertion}

Você pode habilitar uma experiência de TV de poder participar no meio de um anúncio, em fluxos ao vivo. O recurso de quebra parcial de anúncio permite que você imite uma experiência semelhante à TV, na qual, se o cliente iniciar um fluxo ao vivo dentro de um midroll, ele será iniciado dentro desse midroll. É como mudar para um canal de TV e os comerciais funcionam perfeitamente.

Por exemplo, se um usuário ingressar no meio de uma pausa de anúncio de 90 segundos (três anúncios de 30 segundos), 10 segundos após a segunda publicidade (ou seja, 40 segundos após a pausa), ocorrerá o seguinte:

* O segundo anúncio é reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.
* Os rastreadores de anúncios para o anúncio parcialmente reproduzido (o segundo anúncio) não são acionados. Somente o rastreador do terceiro anúncio é disparado.

Esse comportamento não é ativado por padrão. Para ativar esse recurso no aplicativo, faça o seguinte:

Ative a preferência para Inserção parcial de quebra de anúncio. Use o novo método `setPartialAdBreakPref` na interface do MediaPlayer para ativar esse recurso. Use o `getPartialAdBreakPref` método para localizar o estado atual dessa preferência.

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

O anúncio precedente, se disponível, é reproduzido e o conteúdo é reproduzido a partir do ponto ativo, emulando a experiência da televisão ao vivo.
