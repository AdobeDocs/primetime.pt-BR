---
title: Implantando o servidor de licenças e a visão geral do empacotador de pastas
description: Implantando o servidor de licenças e a visão geral do empacotador de pastas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Implantando o servidor de licenças e observando a visão geral do empacotador de pastas {#deploying-the-license-server-and-watched-folder-packager-overview}

Copie os arquivos WAR do servidor de licenças para o diretório [!DNL webapps] do Tomcat. Se você já implantou o arquivo WAR, talvez precise excluir manualmente os diretórios WAR descompactados ( [!DNL flashaccess], [!DNL edcws] e [!DNL flashaccess-packager] no diretório [!DNL webapps] do Tomcat). Para impedir que o Tomcat descompacte arquivos WAR, edite o arquivo [!DNL server.xml] no diretório conf do Tomcat e defina o atributo `unpackWARs` para `false`.

O arquivo de propriedades ( [!DNL flashaccess-refimpl.properties]) deve estar no caminho de classe para que o servidor carregue as propriedades. Copie esse arquivo para um diretório e atualize o arquivo com os valores apropriados. Edite o arquivo [!DNL catalina.properties] no diretório [!DNL conf] do Tomcat e adicione o diretório que contém [!DNL flashaccess-refimpl.properties] à propriedade `shared.loader`. O arquivo [!DNL log4j.xml] para configurar o log também deve estar no classpath (consulte [!DNL resources\log4j.xml] para obter um exemplo).

O servidor de implementação de referência usa vários arquivos de certificado, arquivos de política e outros recursos. Esses arquivos estão todos localizados em uma pasta de recursos. Por padrão, a pasta de recursos é [!DNL C:\flashaccess-server-resources], mas esse local pode ser modificado em [!DNL flashaccess-refimpl.properties]. Certifique-se de copiar todos os recursos necessários para este local antes de iniciar o servidor.

Para iniciar o Tomcat e o servidor de licenças, execute `catalina.bat start` a partir do diretório [!DNL bin] do Tomcat.
