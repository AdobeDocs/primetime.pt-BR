---
title: Versão mínima do cliente
description: Versão mínima do cliente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Versão mínima do cliente {#minimum-client-version}

O Adobe Primetime DRM 2.0.2 e versões posteriores apresentam algumas novas regras de uso, que não são compreendidas pelos clientes do Primetime DRM 2.0. Ao definir a versão mínima suportada do cliente ( `HandlerConfiguration.setMinSupportedClientVersion()`), o servidor de licença pode controlar como os clientes mais antigos se comportam quando encontram licenças com essas regras de uso. Com base nessa configuração, o servidor pode indicar se os clientes mais antigos podem ignorar as regras de uso que não compreendem ou se os clientes mais antigos não poderão consumir licenças com essas regras de uso.

Por exemplo,

* Se a licença especificar os requisitos de recursos do dispositivo ( [Recursos do dispositivo necessários para reproduzir conteúdo protegido](../../../protecting-content/introduction/usage-rules/runtime-application-restrictions/device-capabilities.md)), os clientes DRM Primetime 2.0.2 e superiores podem aplicar esses requisitos.
* Se o servidor de licença não quiser que o conteúdo seja reproduzido em clientes que não compreendem os requisitos de recursos do dispositivo, defina a versão mínima compatível do cliente como 2 (para 2.0.2). Isso impedirá que o servidor emita licenças para clientes DRM do Primetime anteriores à versão 2.0.2. A versão mínima do cliente também será aplicada se a licença for transferida de um cliente para outro.
* Se o servidor de licença quiser permitir que clientes mais antigos ignorem os requisitos de recursos do dispositivo, defina a versão mínima do cliente compatível como 1 (para o Primetime DRM 2.0). Em seguida, o servidor emite uma licença para qualquer cliente versão 2.0 e superior. Se o cliente atualizar ou transferir a licença para outro cliente com a versão 2.0.2 ou posterior, os requisitos de recursos do dispositivo na licença serão aplicados, pois o cliente poderá dar suporte a essa regra de uso.
