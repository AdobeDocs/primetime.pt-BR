---
description: Você pode controlar a visibilidade de legendas ocultas. Quando a visibilidade está ativada, a faixa selecionada no momento é exibida.
title: Controle a visibilidade da legenda oculta
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Controlar visibilidade de legenda fechada{#control-closed-caption-visibility}

Você pode controlar a visibilidade de legendas ocultas. Quando a visibilidade está ativada, a faixa selecionada no momento é exibida.

>[!TIP]
>
>Se você alterar qual rastreamento é atual, a configuração de visibilidade permanecerá a mesma.

Se o texto da legenda fechada for exibido quando o reprodutor entrar no modo de busca, o texto não será mais exibido após a conclusão da busca. Em vez disso, após alguns segundos, o TVSDK do navegador exibe o próximo texto da legenda fechada no vídeo após a posição final da busca.

>[!TIP]
>
>Os valores de visibilidade de legendas ocultas são controlados com `MediaPlayer.VISIBLE` e `MediaPlayer.INVISIBLE`.

1. Use a propriedade `MediaPlayer.ccVisibility` para acessar a configuração de visibilidade atual das legendas ocultas.

