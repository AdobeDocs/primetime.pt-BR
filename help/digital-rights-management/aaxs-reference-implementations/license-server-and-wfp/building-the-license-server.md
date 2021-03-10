---
title: Criação do servidor de licenças
description: Criação do servidor de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Criação do servidor de licenças {#building-the-license-server}

O servidor de licença de implementação de referência inclui arquivos WAR para implantar o servidor de licença. Ele também inclui todo o código fonte do servidor de licenças e um script de compilação Ant (Referência Implementation\Server\refimpl\build-refimpl.xml) para que você possa fazer alterações facilmente no código.

>[!NOTE]
>
>Essa etapa só é necessária se você quiser modificar o código-fonte. Para fins de avaliação, você pode ignorar esta etapa e usar os arquivos WAR conforme enviados.

Antes de executar o script Ant, modifique o script para especificar os locais do SDK do Adobe Access, Tomcat, MySQL e Log4J. Abra build-refimpl.xml em um editor de texto e edite os valores das propriedades `sdkdir, tomcatdir, mysqldir, and log4jdir`. Para compilar o código-fonte e criar os arquivos WAR para a implementação de referência, execute o script usando `ant -f build-refimpl.xml all` no diretório que contém o script Ant. Quando o script for concluído, um diretório [!DNL refimpl-build/wars] contendo os arquivos WAR do servidor será criado.
