---
description: A proteção de repetição impede que um invasor reproduza uma mensagem de solicitação de licença e possivelmente causa um ataque de negação de serviço (DoS) contra o cliente.
seo-description: A proteção de repetição impede que um invasor reproduza uma mensagem de solicitação de licença e possivelmente causa um ataque de negação de serviço (DoS) contra o cliente.
seo-title: Proteção contra repetição
title: Proteção contra repetição
uuid: 93749dd3-a42c-4866-ac54-1b20d6683c42
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Proteção contra repetição{#replay-protection}

A proteção de repetição impede que um invasor reproduza uma mensagem de solicitação de licença e possivelmente causa um ataque de negação de serviço (DoS) contra o cliente.

Um ataque do DoS é uma tentativa dos atacantes de impedir que usuários legítimos de um serviço usem esse serviço. Por exemplo, um ataque de repetição que usa o contador de reversão poderia ser usado para &quot;enganar&quot; o License Server e pensar que o cliente DRM reverteu seu estado, o que causa uma suspensão da conta.

Para saber mais sobre a proteção de repetição, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
