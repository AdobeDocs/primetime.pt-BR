---
title: Dados de configuração do servidor global
description: Dados de configuração do servidor global
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Dados de configuração do servidor global{#global-server-configuration-data}

Além da configuração usada pelo servidor de licenças, `HandlerConfiguration` armazena informações de configuração que podem ser enviadas ao cliente para controlar como as licenças são aplicadas. Isso é feito criando um `ServerConfigData` classe e chamada `HandlerConfiguration.setServerConfigData()`. Estas configurações aplicam-se somente às licenças emitidas por este servidor de licenças.

A tolerância do retrocesso do relógio é uma propriedade que pode ser definida pelo servidor de licenças para controlar como o cliente impõe licenças. Por padrão, os usuários podem atrasar o relógio da máquina 4 horas sem invalidar as licenças. Se um operador de servidor de licenças desejar usar uma configuração diferente, o novo valor poderá ser definido na variável `ServerConfigData` classe. Ao alterar o valor de qualquer uma dessas configurações, certifique-se de incrementar o número da versão chamando `setVersion()`. Os novos valores só serão enviados ao cliente se a versão no cliente for anterior à atual `ServerConfigData` versão.
