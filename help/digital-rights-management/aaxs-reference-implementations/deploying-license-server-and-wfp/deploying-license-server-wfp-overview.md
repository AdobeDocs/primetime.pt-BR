---
title: Visão geral da implantação do servidor de licenças e do empacotador de pastas observado
description: Visão geral da implantação do servidor de licenças e do empacotador de pastas observado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Visão geral da implantação do servidor de licenças e do empacotador de pastas observado {#deploying-the-license-server-and-watched-folder-packager-overview}

Copie os arquivos WAR do servidor de licenças para o Tomcat [!DNL webapps] diretório. Se você tiver implantado anteriormente o arquivo WAR, talvez seja necessário excluir manualmente os diretórios WAR desempacotados ( [!DNL flashaccess], [!DNL edcws], e [!DNL flashaccess-packager] no do Tomcat [!DNL webapps] diretório). Para evitar que o Tomcat descompacte arquivos WAR, edite o [!DNL server.xml] arquivo no diretório conf do Tomcat e defina o `unpackWARs` atributo para `false`.

O arquivo de propriedades ( [!DNL flashaccess-refimpl.properties]) deve estar no classpath para que o servidor carregue as propriedades. Copie este arquivo para um diretório e atualize o arquivo com os valores apropriados. Edite o [!DNL catalina.properties] arquivo no do Tomcat [!DNL conf] e adicione o diretório que contém [!DNL flashaccess-refimpl.properties] para o `shared.loader` propriedade. A variável [!DNL log4j.xml] para configurar o registro também deve estar no classpath (consulte [!DNL resources\log4j.xml] por exemplo).

O servidor de implementação de referência usa vários arquivos de certificado, arquivos de política e outros recursos. Todos esses arquivos estão localizados em uma pasta de recursos. Por padrão, a pasta de recursos é [!DNL C:\flashaccess-server-resources], mas esse local pode ser modificado no [!DNL flashaccess-refimpl.properties]. Certifique-se de copiar todos os recursos necessários para este local antes de iniciar o servidor.

Para iniciar o Tomcat e o servidor de licenças, execute `catalina.bat start` do Tomcat [!DNL bin] diretório.
