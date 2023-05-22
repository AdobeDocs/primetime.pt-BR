---
description: Você pode invocar a lógica de autorização personalizada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.
title: Extensões de autorização personalizadas
exl-id: dbdda9c6-32bf-4904-981f-0029bf0a82f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# Extensões de autorização personalizadas{#custom-authorization-extensions}

Você pode invocar a lógica de autorização personalizada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.

Se quiser implementar sua própria extensão de autorização do cliente, primeiro consulte o [!DNL SampleAuthorizer.java] código de amostra que está localizado no diretório samples. A versão compilada desta amostra está localizada em [!DNL flashaccess-license-server-ext-sample.jar].

Se quiser criar sua própria extensão, é necessário implementar o `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e verifique se [!DNL flashaccess-license-server-exts.jar] e [!DNL commons-logging.jar] estão no caminho de criação ( [!DNL adobe-flashaccess-sdk.jar] também deve estar no caminho de criação se você usar determinados campos no `IMessageFacade`).

Se quiser implantar sua extensão, será necessário copiar os arquivos jar ou de classe para *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/libs].

Se quiser atualizar os arquivos jar ou de classe, é necessário reiniciar o servidor antes que a versão atualizada possa ser usada. Você também deve adicionar o nome da classe do autorizador ao arquivo de configuração do locatário.
