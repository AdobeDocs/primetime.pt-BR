---
seo-title: Extensões de autorização personalizadas
title: Extensões de autorização personalizadas
description: A lógica de autorização personalizada pode ser invocada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.
seo-description: A lógica de autorização personalizada pode ser invocada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.
uuid: fb40db6f-30aa-46e3-9eeb-faff3cfedab1
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Extensões de autorização personalizadas {#custom-authorization-extensions}

A lógica de autorização personalizada pode ser invocada durante a aquisição da licença para decidir se uma licença deve ser emitida para o cliente solicitante.

Para implementar sua própria extensão de autorização do cliente, verifique primeiro o código de amostra [!DNL SampleAuthorizer.java] localizado no diretório samples (a versão compilada dessa amostra está localizada em flashaccess-license-server-ext-sample.jar).

Para criar sua própria extensão, implemente a interface `com.adobe.flashaccess.server.license.extension.auth.IAuthorizer` e verifique se `flashaccess-license-server-exts.jar` e `commons-logging.jar` estão no caminho de compilação `adobe-flashaccess-sdk.jar` também devem estar no caminho de compilação se você utilizar determinados campos em `IMessageFacade`). Para implantar sua extensão, copie seus arquivos jar ou de classe para *LicenseServer.ConfigRoot* `/flashaccessserver/libs`. Se você precisar atualizar os arquivos jar ou de classe, o servidor deverá ser reiniciado antes que a versão atualizada seja usada. Você também deve adicionar o nome da classe do autorizador ao arquivo de configuração do locatário.
