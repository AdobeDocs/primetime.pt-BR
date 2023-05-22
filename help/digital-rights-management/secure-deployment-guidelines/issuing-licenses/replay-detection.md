---
description: A proteção contra repetição impede que um invasor reproduza uma mensagem de solicitação de licença e, possivelmente, cause um ataque de negação de serviço (DoS) contra o cliente.
title: Proteção contra repetição
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Proteção contra repetição{#replay-protection}

A proteção contra repetição impede que um invasor reproduza uma mensagem de solicitação de licença e, possivelmente, cause um ataque de negação de serviço (DoS) contra o cliente.

Um ataque de DoS é uma tentativa dos invasores de impedir que usuários legítimos de um serviço usem esse serviço. Por exemplo, um ataque de repetição que usa o contador de reversão pode ser usado para &quot;enganar&quot; o License Server para que ele pense que o cliente DRM reverteu seu estado, o que causa uma suspensão da conta.

Para saber mais sobre a proteção de repetição, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
