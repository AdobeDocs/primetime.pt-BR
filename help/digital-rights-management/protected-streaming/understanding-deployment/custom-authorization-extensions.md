---
description: Você pode invocar a lógica de autorização personalizada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.
seo-description: Você pode invocar a lógica de autorização personalizada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.
seo-title: Extensões de autorização personalizadas
title: Extensões de autorização personalizadas
uuid: 588b05e5-3402-4586-bbd4-58b7e9a58ee4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Extensões de autorização personalizadas{#custom-authorization-extensions}

Você pode invocar a lógica de autorização personalizada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.

Se você quiser implementar sua própria extensão de autorização do cliente, verifique primeiro o código de amostra [!DNL SampleAuthorizer.java] localizado no diretório samples. A versão compilada desta amostra está localizada em [!DNL flashaccess-license-server-ext-sample.jar].

Se quiser criar sua própria extensão, você precisa implementar a interface `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e verificar se [!DNL flashaccess-license-server-exts.jar] e [!DNL commons-logging.jar] estão no caminho de compilação ( [!DNL adobe-flashaccess-sdk.jar] também deve estar no caminho de compilação se você usar determinados campos em `IMessageFacade`).

Se desejar implantar sua extensão, você precisa copiar os arquivos jar ou de classe para *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Se quiser atualizar os arquivos jar ou class, reinicie o servidor antes que a versão atualizada possa ser usada. Você também deve adicionar o nome da classe do autorizador ao arquivo de configuração do locatário.
