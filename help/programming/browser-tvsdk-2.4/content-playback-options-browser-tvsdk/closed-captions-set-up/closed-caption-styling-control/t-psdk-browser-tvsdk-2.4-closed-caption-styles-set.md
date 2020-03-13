---
description: É possível definir o formato, como fonte, tamanho, cor, borda e opacidade para texto de legenda.
seo-description: É possível definir o formato, como fonte, tamanho, cor, borda e opacidade para texto de legenda.
seo-title: Definir estilos de legenda
title: Definir estilos de legenda
uuid: 906ed22c-e673-4211-a14b-d95d176aad21
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Definir estilos de legenda{#set-closed-caption-styles}

É possível definir o formato, como fonte, tamanho, cor, borda e opacidade para texto de legenda.

1. Aguarde até `MediaPlayer` o estado PREPARADO.

   Para obter mais informações sobre os estados, consulte [Aguardar um estado](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md)válido.
1. Crie uma `TextFormat` instância.

   Você pode fornecer todos os parâmetros de estilo de legenda agora ou defini-los posteriormente.

   ```js
   new TextFormat( 
       font,   
       fontColor,  
       edgeColor,   
       fontEdge,  
       backgroundColor,   
       fillColor,  
       size,   
       fontOpacity,   
       backgroundOpacity,  
       fillOpacity, 
       bottomInset 
       safeArea) → {AdobePSDK.TextFormat}
   ```

1. (Opcional) Obtenha as configurações atuais de estilo de legenda fechada com `MediaPlayer.ccStyle`.

   O valor de retorno é uma instância da `TextFormat` interface.

   Se nenhum estilo tiver sido definido anteriormente, ele retornará um objeto TextFormat com valores padrão para cada atributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Para alterar as configurações de estilo, use `MediaPlayer.ccStyle`, transmitindo uma instância da `TextFormat` interface.

   Você pode usar esse método mesmo se o fluxo de mídia atual não tiver legendas fechadas.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >A configuração do estilo de legenda fechada é assíncrona, portanto, pode levar alguns segundos para que as alterações sejam exibidas na tela.

