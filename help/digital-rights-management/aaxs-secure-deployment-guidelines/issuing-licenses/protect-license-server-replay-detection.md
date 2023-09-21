---
title: Proteção contra repetição
description: Proteção contra repetição
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Proteção contra repetição{#replay-protection}

A proteção contra repetição impede que um invasor reproduza uma mensagem de solicitação de licença e, possivelmente, cause um ataque de negação de serviço (DoS) contra o cliente (A *negação de serviço* ataque é uma tentativa de invasores de impedir que usuários legítimos de um serviço usem esse serviço). Por exemplo, um ataque de repetição usando o contador de reversão pode ser usado para &quot;enganar&quot; o License Server para que ele pense que o cliente DRM está revertendo seu estado, causando uma suspensão da conta.

Para saber mais sobre a proteção de repetição, consulte `AbstractRequestMessage.getMessageId()` o *Referência da API de acesso do Adobe*.
