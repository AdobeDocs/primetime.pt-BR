---
seo-title: Proteção contra repetição
title: Proteção contra repetição
uuid: 5e6488e6-0834-4dcf-bc26-55019f5db320
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Reproduzir proteção{#replay-protection}

A proteção de repetição impede que um invasor reproduza uma mensagem de solicitação de licença e possivelmente causa um ataque de negação de serviço (DoS) contra o cliente (um ataque de *negação de serviço* é uma tentativa dos atacantes de impedir que usuários legítimos de um serviço usem esse serviço). Por exemplo, um ataque de repetição usando o contador de reversão poderia ser usado para &quot;enganar&quot; o License Server e pensar que o cliente DRM está revertendo seu estado, causando uma suspensão da conta.

Para saber mais sobre a proteção de repetição, consulte `AbstractRequestMessage.getMessageId()` a *Referência da API de Acesso ao Adobe*.
