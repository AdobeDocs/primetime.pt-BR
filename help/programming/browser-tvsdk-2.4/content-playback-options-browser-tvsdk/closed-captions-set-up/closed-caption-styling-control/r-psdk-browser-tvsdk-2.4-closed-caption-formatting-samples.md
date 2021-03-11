---
description: É possível especificar a formatação de legenda oculta.
title: Exemplos de formatação de legenda
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '33'
ht-degree: 0%

---


# Exemplos: Formatação de legenda{#examples-caption-formatting}

É possível especificar a formatação de legenda oculta.

## Exemplo 1: Especificar valores de formato explicitamente {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```js
// Set CC style. 
var tf = new AdobePSDK.TextFormat( 
      AdobePSDK.TextFormat.FONT_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.FONT_EDGE_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.SIZE_DEFAULT, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY; 
 mediaPlayer.CCStyle(tf);
```

>[!IMPORTANT]
>
>O TVSDK do navegador não oferece suporte à borda da fonte, cor de preenchimento ou opacidade de preenchimento.

