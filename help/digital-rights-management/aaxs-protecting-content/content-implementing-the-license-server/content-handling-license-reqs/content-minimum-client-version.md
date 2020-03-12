---
seo-title: Versão mínima do cliente
title: Versão mínima do cliente
uuid: 9f39e4e7-64eb-43ea-b194-b744838a411e
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Versão mínima do cliente {#minimum-client-version}

O Adobe Access 2.0.2 e superior apresenta algumas novas regras de uso, que não são entendidas pelos clientes do Adobe Access 2.0. Ao definir a versão mínima compatível do cliente ( `HandlerConfiguration.setMinSupportedClientVersion()`), o servidor de licenças pode controlar como os clientes mais antigos se comportarão quando encontrarem licenças com essas regras de uso. Com base nessa configuração, o servidor pode indicar se os clientes mais antigos podem ignorar as regras de uso que não entendem ou se os clientes mais antigos não poderão consumir licenças com essas regras de uso.

Por exemplo,

* Se a licença especificar os requisitos de recursos do dispositivo (recursos do [dispositivo necessários para reproduzir conteúdo](../../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-device-capabilities.md)protegido), os clientes do Adobe Access 2.0.2 e superior poderão aplicar esses requisitos.
* Se o servidor de licenças não quiser que o conteúdo seja reproduzido em clientes que não compreendem os requisitos de recursos do dispositivo, defina a versão mínima do cliente compatível como 2 (para 2.0.2). Isso impedirá que o servidor emita licenças para clientes do Adobe Access antes da versão 2.0.2. A versão mínima do cliente também será imposta se a licença for transferida de um cliente para outro.
* Se o servidor de licenças quiser permitir que clientes antigos ignorem os requisitos de recursos do dispositivo, defina a versão mínima do cliente compatível como 1 (para o Adobe Access 2.0). O servidor emitirá uma licença para qualquer versão do cliente 2.0 ou superior. Se o cliente atualizar ou transferir a licença para outro cliente com a versão 2.0.2 ou superior, os requisitos de recursos do dispositivo na licença serão aplicados, já que o cliente agora suportaria essa regra de uso.

