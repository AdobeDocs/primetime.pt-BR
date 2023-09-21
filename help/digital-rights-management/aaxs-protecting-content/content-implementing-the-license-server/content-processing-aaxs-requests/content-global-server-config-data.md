---
title: Dados de configuração do servidor global
description: Dados de configuração do servidor global
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Dados de configuração do servidor global{#global-server-configuration-data}

Além da configuração usada pelo servidor de licenças, `HandlerConfiguration` armazena informações de configuração que podem ser enviadas ao cliente para controlar como as licenças são aplicadas. Isso é feito criando um `ServerConfigData` classe e chamada `HandlerConfiguration.setServerConfigData()` (essas configurações se aplicam somente às licenças emitidas por este servidor de licenças). A tolerância do retrocesso do relógio é uma propriedade que pode ser definida pelo servidor de licenças para controlar como o cliente impõe licenças. Por padrão, os usuários podem atrasar o relógio da máquina 4 horas sem invalidar as licenças. Se um operador de servidor de licenças desejar usar uma configuração diferente, o novo valor poderá ser definido na variável `ServerConfigData` classe. Ao alterar o valor de qualquer uma dessas configurações, certifique-se de incrementar o número da versão chamando `setVersion()`. Os novos valores só serão enviados ao cliente se a versão no cliente for menor que a atual `ServerConfigData` versão.
