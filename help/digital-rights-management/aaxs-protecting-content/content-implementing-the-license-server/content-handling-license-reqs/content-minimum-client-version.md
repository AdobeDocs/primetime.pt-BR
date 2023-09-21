---
title: Versão Mínima do Cliente
description: Versão Mínima do Cliente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Versão Mínima do Cliente {#minimum-client-version}

Adobe Access 2.0.2 e superior introduzem algumas novas regras de uso, que não são compreendidas pelos clientes do Adobe Access 2.0. Ao definir a versão mínima suportada do cliente ( `HandlerConfiguration.setMinSupportedClientVersion()`), o servidor de licença pode controlar como os clientes mais antigos se comportarão quando encontrarem licenças com essas regras de uso. Com base nessa configuração, o servidor pode indicar se os clientes mais antigos podem ignorar as regras de uso que não compreendem ou se os clientes mais antigos não poderão consumir licenças com essas regras de uso.

Por exemplo,

* Se a licença especificar os requisitos de recursos do dispositivo ( [Recursos do dispositivo necessários para reproduzir conteúdo protegido](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)), os clientes do Adobe Access 2.0.2 e superior podem aplicar esses requisitos.
* Se o servidor de licença não quiser que o conteúdo seja reproduzido em clientes que não compreendem os requisitos de recursos do dispositivo, defina a versão mínima compatível do cliente como 2 (para 2.0.2). Isso impedirá que o servidor emita licenças para os clientes do Adobe Access anteriores à versão 2.0.2. A versão mínima do cliente também será aplicada se a licença for transferida de um cliente para outro.
* Se o servidor de licença quiser permitir que clientes mais antigos ignorem os requisitos de recursos do dispositivo, defina a versão mínima suportada do cliente como 1 (para o Adobe Access 2.0). O servidor emitirá uma licença para qualquer versão de cliente 2.0 e superior. Se o cliente atualizar ou transferir a licença para outro cliente com a versão 2.0.2 ou superior, os requisitos de recursos do dispositivo na licença serão aplicados, pois o cliente oferecerá suporte a essa regra de uso.
