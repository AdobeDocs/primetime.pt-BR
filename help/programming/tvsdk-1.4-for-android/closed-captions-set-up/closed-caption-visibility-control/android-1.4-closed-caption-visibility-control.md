---
description: Você pode controlar a visibilidade de legendas ocultas. Quando a visibilidade está ativada, a faixa selecionada no momento é exibida. Se você alterar qual rastreamento é atual, a configuração de visibilidade permanecerá a mesma.
title: Controle a visibilidade da legenda oculta
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---


# Visão geral {#control-closed-caption-visibility}

Você pode controlar a visibilidade de legendas ocultas. Quando a visibilidade está ativada, a faixa selecionada no momento é exibida. Se você alterar qual rastreamento é atual, a configuração de visibilidade permanecerá a mesma.

>[!TIP]
>
>Se o texto da legenda fechada for exibido quando o reprodutor entrar no modo de busca, o texto não será mais exibido após a conclusão da busca. Em vez disso, após alguns segundos, o TVSDK exibe o próximo texto da legenda fechada no vídeo após a posição final da busca.

>[!NOTE]
>
>Os valores de visibilidade para legendas ocultas são definidos em `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Aguarde até que o MediaPlayer tenha pelo menos o estado PREPARADO (consulte [Aguarde um estado válido](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Para obter a configuração de visibilidade atual das legendas ocultas, use o método getter no MediaPlayer, que retorna um valor de visibilidade.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Para alterar a visibilidade de legendas ocultas, use o método setter, transmitindo um valor de visibilidade de `MediaPlayer.Visibility`.

   Por exemplo:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

