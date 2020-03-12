---
description: É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade é ativada, a faixa selecionada no momento é exibida. Se você alterar qual faixa é atual, a configuração de visibilidade permanecerá a mesma.
seo-description: É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade é ativada, a faixa selecionada no momento é exibida. Se você alterar qual faixa é atual, a configuração de visibilidade permanecerá a mesma.
seo-title: Controlar a visibilidade da legenda
title: Controlar a visibilidade da legenda
uuid: f142e60d-5581-4d1c-9d4d-a4a58ac1b67b
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Controlar a visibilidade da legenda {#control-closed-caption-visibility}

É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade é ativada, a faixa selecionada no momento é exibida. Se você alterar qual faixa é atual, a configuração de visibilidade permanecerá a mesma.

>[!TIP]
>
>Se o texto da legenda fechada for exibido quando o player entrar no modo de busca, o texto não será mais exibido depois que a busca for concluída. Em vez disso, após alguns segundos, o TVSDK exibe o próximo texto de legenda fechada no vídeo após a posição de busca final.
>
>Os valores de visibilidade para legendas fechadas são definidos em `MediaPlayer.Visibility`. >
>
```java>
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```>



1. Aguarde até `MediaPlayer` o estado PREPARADO. Para obter mais informações, consulte [Aguardar um status](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md)válido.

1. Para obter a configuração de visibilidade atual de legendas fechadas, use o método getter em `MediaPlayer`, que retorna um valor de visibilidade.

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. Para alterar a visibilidade de legendas fechadas, use o método setter, transmitindo um valor de visibilidade de `MediaPlayer.Visibility`.

   Por exemplo:

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
