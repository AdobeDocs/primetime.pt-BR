---
description: É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida.
seo-description: É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida.
seo-title: Controlar a visibilidade da legenda
title: Controlar a visibilidade da legenda
uuid: b161a729-73f3-4019-a95e-013b42779842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Controlar visibilidade de legenda fechada{#control-closed-caption-visibility}

É possível controlar a visibilidade das legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida.

>[!TIP]
>
>Se você alterar qual faixa é atual, a configuração de visibilidade permanecerá a mesma.

Se o texto da legenda fechada for exibido quando o player entrar no modo de busca, o texto não será mais exibido depois que a busca for concluída. Em vez disso, após alguns segundos, o TVSDK do navegador exibe o próximo texto de legenda fechada no vídeo após a posição de busca final.

>[!TIP]
>
>Os valores de visibilidade para legendas fechadas são controlados com `MediaPlayer.VISIBLE` e `MediaPlayer.INVISIBLE`.

1. Use a propriedade `MediaPlayer.ccVisibility` para acessar a configuração de visibilidade atual das legendas fechadas.

