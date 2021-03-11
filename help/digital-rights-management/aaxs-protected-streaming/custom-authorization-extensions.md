---
title: Extensões de autorização personalizadas
description: A lógica de autorização personalizada pode ser invocada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente requerente.
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Extensões de autorização personalizadas {#custom-authorization-extensions}

A lógica de autorização personalizada pode ser invocada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente requerente.

Para implementar sua própria extensão de autorização do cliente, verifique primeiro o código de amostra [!DNL SampleAuthorizer.java] localizado no diretório de amostras (a versão compilada dessa amostra está localizada em flashaccess-license-server-ext-sample.jar).

Para criar sua própria extensão, implemente a interface `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e verifique se `flashaccess-license-server-exts.jar` e `commons-logging.jar` estão no caminho de compilação `adobe-flashaccess-sdk.jar` também devem estar no caminho de compilação se você utilizar determinados campos em `IMessageFacade`). Para implantar sua extensão, copie seu jar ou arquivos de classe para *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Se você precisar atualizar os arquivos jar ou de classe, o servidor deverá ser reiniciado antes que a versão atualizada seja usada. Você também deve adicionar o nome da classe authorizer ao arquivo de configuração do locatário.
