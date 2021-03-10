---
description: É possível definir o formato, como fonte, tamanho, cor, borda e opacidade para texto de legenda.
title: Definir estilos de legenda
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Definir estilos de legenda fechada{#set-closed-caption-styles}

É possível definir o formato, como fonte, tamanho, cor, borda e opacidade para texto de legenda.

1. Aguarde até que `MediaPlayer` esteja pelo menos no estado PREPARADO.

   Para obter mais informações sobre os estados, consulte [Aguardar um estado válido](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Crie uma instância `TextFormat`.

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

1. (Opcional) Obtenha as configurações atuais de estilo de legenda com `MediaPlayer.ccStyle`.

   O valor de retorno é uma instância da interface `TextFormat`.

   Se nenhum estilo tiver sido definido anteriormente, ele retornará um objeto TextFormat com valores padrão para cada atributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Para alterar as configurações de estilo, use `MediaPlayer.ccStyle`, transmitindo uma instância da interface `TextFormat`.

   Você pode usar esse método mesmo se o fluxo de mídia atual não tiver legendas ocultas.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >A configuração do estilo de legenda oculta é assíncrona, portanto, pode levar alguns segundos para que as alterações sejam exibidas na tela.

