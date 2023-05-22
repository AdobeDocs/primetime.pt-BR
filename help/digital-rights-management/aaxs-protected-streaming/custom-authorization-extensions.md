---
title: Extensões de autorização personalizadas
description: A lógica de autorização personalizada pode ser invocada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.
exl-id: bf7870f5-11bf-4392-a422-506b47d684f9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Extensões de autorização personalizadas {#custom-authorization-extensions}

A lógica de autorização personalizada pode ser invocada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.

Para implementar sua própria extensão de autorização do cliente, verifique primeiro o [!DNL SampleAuthorizer.java] código de amostra localizado no diretório samples (a versão compilada deste exemplo está localizada em flashaccess-license-server-ext-sample.jar).

Para criar sua própria extensão, implemente o `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e verifique se `flashaccess-license-server-exts.jar` e `commons-logging.jar` estão no caminho de criação `adobe-flashaccess-sdk.jar` também deve estar no caminho de criação se você utilizar determinados campos no `IMessageFacade`). Para implantar sua extensão, copie os arquivos jar ou de classe em *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Se você precisar atualizar os arquivos jar ou de classe, o servidor deve ser reiniciado antes que a versão atualizada seja usada. Você também deve adicionar o nome da classe do autorizador ao arquivo de configuração do locatário.
