---
description: Você pode invocar a lógica de autorização personalizada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.
title: Extensões de autorização personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Extensões de autorização personalizadas{#custom-authorization-extensions}

Você pode invocar a lógica de autorização personalizada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.

Se quiser implementar sua própria extensão de autorização do cliente, primeiro verifique o código de amostra [!DNL SampleAuthorizer.java] localizado no diretório de amostras. A versão compilada desta amostra está localizada em [!DNL flashaccess-license-server-ext-sample.jar].

Se quiser criar sua própria extensão, é necessário implementar a interface `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e garantir que [!DNL flashaccess-license-server-exts.jar] e [!DNL commons-logging.jar] estejam no caminho de compilação ( [!DNL adobe-flashaccess-sdk.jar] também deve estar no caminho de compilação se você usar determinados campos em `IMessageFacade`).

Se quiser implantar sua extensão, você precisa copiar o jar ou os arquivos de classe para *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Se quiser atualizar os arquivos jar ou class, é necessário reiniciar o servidor antes que a versão atualizada possa ser usada. Você também deve adicionar o nome da classe authorizer ao arquivo de configuração do locatário.
