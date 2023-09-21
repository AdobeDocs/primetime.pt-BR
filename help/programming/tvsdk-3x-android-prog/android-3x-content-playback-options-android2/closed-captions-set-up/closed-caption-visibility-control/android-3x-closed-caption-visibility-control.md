---
description: É possível controlar a visibilidade de legendas ocultas. Quando a visibilidade for ativada, a faixa selecionada no momento será exibida. Se você alterar a faixa atual, a configuração de visibilidade permanecerá a mesma.
title: Controlar visibilidade de legendas ocultas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Controlar visibilidade de legendas ocultas {#control-closed-caption-visibility}

É possível controlar a visibilidade de legendas ocultas. Quando a visibilidade for ativada, a faixa selecionada no momento será exibida. Se você alterar a faixa atual, a configuração de visibilidade permanecerá a mesma.

>[!TIP]
>
>Se o texto de legendas ocultas for exibido quando o reprodutor entrar no modo de busca, ele não será mais exibido após a conclusão da busca. Em vez disso, após alguns segundos, o TVSDK exibe o próximo texto de legenda oculta no vídeo após a posição de busca final.
>
>Os valores de visibilidade para as legendas ocultas são definidos em `MediaPlayer.Visibility`.
>
>```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```
>

1. Aguarde a `MediaPlayer` estar pelo menos no status PREPARADO. Para obter mais informações, consulte [Aguardar um status válido](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md).

1. Para obter a configuração de visibilidade atual das legendas ocultas, use o método getter em `MediaPlayer`, que retorna um valor de visibilidade.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Para alterar a visibilidade de legendas ocultas, use o método setter, transmitindo um valor de visibilidade de `MediaPlayer.Visibility`.

   Por exemplo:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
