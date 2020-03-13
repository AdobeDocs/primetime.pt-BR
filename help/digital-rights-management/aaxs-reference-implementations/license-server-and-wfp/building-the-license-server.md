---
seo-title: Criação do servidor de licenças
title: Criação do servidor de licenças
uuid: d7ca8a8f-c778-41a2-b823-93fac9ab07c5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Criação do servidor de licenças {#building-the-license-server}

O servidor de licença de implementação de referência inclui arquivos WAR para a implantação do servidor de licenças. Ele também inclui todo o código-fonte do servidor de licenças e um script de construção Ant (Referência Implementation\Server\refimpl\build-refimpl.xml) para que você possa fazer alterações facilmente no código.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Essa etapa só é necessária se você quiser modificar o código-fonte. Para fins de avaliação, você pode ignorar esta etapa e usar os arquivos WAR conforme enviados.

Antes de executar o script Ant, modifique o script para especificar os locais do SDK do Adobe Access, Tomcat, MySQL e Log4J. Abra build-refimpl.xml em um editor de texto e edite os valores das propriedades `sdkdir, tomcatdir, mysqldir, and log4jdir`. Para compilar o código-fonte e criar os arquivos WAR para a implementação de referência, execute o script usando `ant -f build-refimpl.xml all` o diretório que contém o script Ant. Quando o script for concluído, um [!DNL refimpl-build/wars] diretório contendo os arquivos WAR do servidor será criado.
