---
title: Versão mínima do cliente
description: Versão mínima do cliente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# Versão mínima do cliente {#minimum-client-version}

O Adobe Primetime DRM 2.0.2 e superior apresenta algumas novas regras de uso, que não são entendidas pelos clientes do Primetime DRM 2.0. Ao definir a versão mínima compatível do cliente ( `HandlerConfiguration.setMinSupportedClientVersion()`), o servidor de licenças pode controlar como os clientes mais antigos se comportam quando encontram licenças com essas regras de uso. Com base nessa configuração, o servidor pode indicar se os clientes mais antigos podem ignorar as regras de uso que não entendem ou se os clientes mais antigos não poderão consumir licenças com essas regras de uso.

Por exemplo,

* Se a licença especificar os requisitos de recursos do dispositivo ( [Recursos do dispositivo necessários para reproduzir conteúdo protegido](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)), os clientes DRM do Primetime 2.0.2 e superior poderão aplicar esses requisitos.
* Se o servidor de licenças não quiser que o conteúdo seja reproduzido em clientes que não entendem os requisitos de recursos do dispositivo, defina a versão mínima do cliente compatível como 2 (para 2.0.2). Isso impedirá que o servidor emita licenças para clientes DRM Primetime antes da versão 2.0.2. A versão mínima do cliente também é aplicada se a licença for transferida de um cliente para outro.
* Se o servidor de licenças quiser permitir que clientes mais antigos ignorem os requisitos de recursos do dispositivo, defina a versão mínima do cliente compatível como 1 (para Primetime DRM 2.0). Em seguida, o servidor emite uma licença para qualquer cliente versão 2.0 ou superior. Se o cliente atualizar ou transferir a licença para outro cliente com a versão 2.0.2 ou posterior, os requisitos de recursos do dispositivo na licença serão aplicados, pois o cliente pode suportar essa regra de uso.

