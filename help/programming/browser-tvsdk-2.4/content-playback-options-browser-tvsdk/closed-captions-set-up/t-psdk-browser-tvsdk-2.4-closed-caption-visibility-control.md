---
description: É possível controlar a visibilidade de legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida.
title: Controlar visibilidade de legendas ocultas
exl-id: e74c0344-43f3-4ed7-bbf2-d89dd3df8a33
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Controlar visibilidade de legendas ocultas{#control-closed-caption-visibility}

É possível controlar a visibilidade de legendas ocultas. Quando a visibilidade estiver ativada, a faixa selecionada no momento será exibida.

>[!TIP]
>
>Se você alterar a faixa atual, a configuração de visibilidade permanecerá a mesma.

Se o texto de legendas ocultas for exibido quando o reprodutor entrar no modo de busca, ele não será mais exibido após a conclusão da busca. Em vez disso, após alguns segundos, o TVSDK do navegador exibe o próximo texto de legendas ocultas no vídeo após a posição de busca final.

>[!TIP]
>
>Os valores de visibilidade de legendas ocultas são controlados com `MediaPlayer.VISIBLE` e `MediaPlayer.INVISIBLE`.

1. Use o `MediaPlayer.ccVisibility` para acessar a configuração de visibilidade atual das legendas ocultas.
