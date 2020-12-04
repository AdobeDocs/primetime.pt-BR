---
description: É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida. Se você alterar qual faixa é atual, a configuração de visibilidade permanecerá a mesma.
seo-description: É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida. Se você alterar qual faixa é atual, a configuração de visibilidade permanecerá a mesma.
seo-title: Controlar a visibilidade da legenda
title: Controlar a visibilidade da legenda
uuid: 42913347-8158-474e-aa3c-ba4d38baba12
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Visão geral {#control-closed-caption-visibility}

É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida. Se você alterar qual faixa é atual, a configuração de visibilidade permanecerá a mesma.

>[!TIP]
>
>Se o texto da legenda fechada for exibido quando o player entrar no modo de busca, o texto não será mais exibido depois que a busca for concluída. Em vez disso, após alguns segundos, o TVSDK exibe o próximo texto de legenda fechada no vídeo após a posição de busca final.

>[!NOTE]
>
>Os valores de visibilidade para legendas fechadas são definidos em `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. Aguarde até que o MediaPlayer tenha pelo menos o estado PREPARED (consulte [Aguardar um estado válido](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. Para obter a configuração de visibilidade atual de legendas fechadas, use o método getter no MediaPlayer, que retorna um valor de visibilidade.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. Para alterar a visibilidade de legendas fechadas, use o método setter, transmitindo um valor de visibilidade de `MediaPlayer.Visibility`.

   Por exemplo:

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

