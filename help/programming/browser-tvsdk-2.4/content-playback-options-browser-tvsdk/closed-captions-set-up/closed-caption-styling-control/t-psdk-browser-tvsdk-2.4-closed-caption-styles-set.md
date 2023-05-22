---
description: É possível definir o formato, como fonte, tamanho, cor, borda e opacidade para texto de legendas ocultas.
title: Definir estilos de legendas ocultas
exl-id: 7ece68ce-0dc5-4899-9834-39940bbd0332
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Definir estilos de legendas ocultas{#set-closed-caption-styles}

É possível definir o formato, como fonte, tamanho, cor, borda e opacidade para texto de legendas ocultas.

1. Aguarde a `MediaPlayer` estar pelo menos no estado PREPARADO.

   Para obter mais informações sobre os estados, consulte [Aguardar um estado válido](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Criar um `TextFormat` instância.

   Você pode fornecer todos os parâmetros de estilo de legendas ocultas agora ou defini-los posteriormente.

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

1. (Opcional) Obtenha as configurações de estilo atuais de legendas ocultas com o `MediaPlayer.ccStyle`.

   O valor de retorno é uma instância do `TextFormat` interface.

   Se nenhum estilo tiver sido definido anteriormente, ele retornará um objeto TextFormat com valores padrão para cada atributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Para alterar as configurações de estilo, use `MediaPlayer.ccStyle`, transmitindo uma instância do `TextFormat` interface.

   Você pode usar esse método mesmo se o fluxo de mídia atual não tiver legendas ocultas.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >A definição do estilo de legenda oculta é assíncrona, portanto, pode levar alguns segundos para que as alterações apareçam na tela.
