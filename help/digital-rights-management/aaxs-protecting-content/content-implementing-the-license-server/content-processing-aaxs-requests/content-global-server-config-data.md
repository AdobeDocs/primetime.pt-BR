---
title: Dados de configuração do servidor global
description: Dados de configuração do servidor global
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Dados de configuração do servidor global{#global-server-configuration-data}

Além da configuração usada pelo servidor de licenças, `HandlerConfiguration` armazena informações de configuração que podem ser enviadas ao cliente para controlar como as licenças são aplicadas. Isso é feito criando uma classe `ServerConfigData` e chamando `HandlerConfiguration.setServerConfigData()` (essas configurações se aplicam somente às licenças emitidas por esse servidor de licenças). A tolerância de retorno de chamada do relógio é uma propriedade que pode ser definida pelo servidor de licença para controlar como o cliente aplica licenças. Por padrão, os usuários podem retornar o relógio da máquina 4 horas sem invalidar licenças. Se um operador de servidor de licenças quiser usar uma configuração diferente, o novo valor poderá ser definido na classe `ServerConfigData`. Ao alterar o valor de qualquer uma dessas configurações, incremente o número da versão chamando `setVersion()`. Os novos valores só serão enviados para o cliente se a versão no cliente for inferior à versão `ServerConfigData` atual.
