---
description: É possível controlar a visibilidade de legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida. Se você alterar a faixa atual, a configuração de visibilidade permanecerá a mesma.
title: Controlar visibilidade de legendas ocultas
exl-id: d9428744-1700-4917-b334-d6e0446eaf37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Visão geral {#control-closed-caption-visibility}

É possível controlar a visibilidade de legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida. Se você alterar a faixa atual, a configuração de visibilidade permanecerá a mesma.

>[!TIP]
>
>Se o texto de legendas ocultas for exibido quando o reprodutor entrar no modo de busca, ele não será mais exibido após a conclusão da busca. Em vez disso, após alguns segundos, o TVSDK exibe o próximo texto de legenda oculta no vídeo após a posição de busca final.

>[!NOTE]
>
>Os valores de visibilidade para as legendas ocultas são definidos em `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Aguarde o MediaPlayer ter pelo menos o estado PREPARADO (consulte [Aguardar um estado válido](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Para obter a configuração de visibilidade atual para legendas ocultas, use o método Getter no MediaPlayer, que retorna um valor de visibilidade.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Para alterar a visibilidade de legendas ocultas, use o método setter, transmitindo um valor de visibilidade de `MediaPlayer.Visibility`.

   Por exemplo:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```
