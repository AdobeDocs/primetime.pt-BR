---
seo-title: Dados de configuração do servidor global
title: Dados de configuração do servidor global
uuid: a1557b3e-9a08-4623-a62d-8ebc308eae15
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Dados de configuração do servidor global{#global-server-configuration-data}

Além da configuração usada pelo servidor de licenças, `HandlerConfiguration` armazena informações de configuração que podem ser enviadas ao cliente para controlar como as licenças são aplicadas. Isso é feito criando uma `ServerConfigData` classe e chamando `HandlerConfiguration.setServerConfigData()`. Essas configurações se aplicam somente às licenças emitidas por este servidor de licenças.

A tolerância de retorno de travamento do relógio é uma propriedade que pode ser definida pelo servidor de licenças para controlar como o cliente aplica licenças. Por padrão, os usuários podem retornar o relógio da máquina 4 horas sem invalidar licenças. Se um operador de servidor de licenças desejar usar uma configuração diferente, o novo valor poderá ser definido na `ServerConfigData` classe. Ao alterar o valor de qualquer uma dessas configurações, certifique-se de aumentar o número da versão chamando `setVersion()`. Os novos valores só serão enviados para o cliente se a versão no cliente for anterior à `ServerConfigData` versão atual.
