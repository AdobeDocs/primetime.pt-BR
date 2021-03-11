---
title: Proteção contra repetição
description: Proteção contra repetição
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Reproduzir proteção{#replay-protection}

A proteção de repetição impede que um invasor reproduza uma mensagem de solicitação de licença e possivelmente causa um ataque de negação de serviço (DoS) contra o cliente (um ataque de *negação de serviço* é uma tentativa de invasores para impedir que usuários legítimos de um serviço usem esse serviço). Por exemplo, um ataque de repetição usando o contador de reversão poderia ser usado para &quot;enganar&quot; o License Server a pensar que o cliente DRM está revertendo seu estado, causando uma suspensão da conta.

Para saber mais sobre a proteção de repetição, consulte `AbstractRequestMessage.getMessageId()` a *Referência da API de Acesso ao Adobe*.
