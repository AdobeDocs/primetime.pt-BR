---
seo-title: Implantação do servidor de licenças e visão geral do empacotador de pastas observado
title: Implantação do servidor de licenças e visão geral do empacotador de pastas observado
uuid: 4b71f2f4-f971-4382-ae41-171f7dfdfe21
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Implantação do servidor de licenças e visão geral do empacotador de pastas assistida {#deploying-the-license-server-and-watched-folder-packager-overview}

Copie os arquivos WAR do servidor de licenças para o diretório [!DNL webapps] do Tomcat. Se você já implantou o arquivo WAR anteriormente, talvez seja necessário excluir manualmente os diretórios WAR descompactados ( [!DNL flashaccess], [!DNL edcws] e [!DNL flashaccess-packager] no diretório [!DNL webapps] do Tomcat). Para impedir que o Tomcat descompacte arquivos WAR, edite o arquivo [!DNL server.xml] no diretório conf do Tomcat e defina o atributo `unpackWARs` como `false`.

O arquivo de propriedades ( [!DNL flashaccess-refimpl.properties]) deve estar no classpath para que o servidor carregue as propriedades. Copie este arquivo para um diretório e atualize-o com os valores apropriados. Edite o arquivo [!DNL catalina.properties] no diretório [!DNL conf] do Tomcat e adicione o diretório que contém [!DNL flashaccess-refimpl.properties] à propriedade `shared.loader`. O arquivo [!DNL log4j.xml] para configurar o registro também deve estar no classpath (consulte [!DNL resources\log4j.xml] para obter um exemplo).

O servidor de implementação de referência usa vários arquivos de certificado, arquivos de política e outros recursos. Esses arquivos estão todos localizados em uma pasta de recursos. Por padrão, a pasta de recursos é [!DNL C:\flashaccess-server-resources], mas esse local pode ser modificado em [!DNL flashaccess-refimpl.properties]. Certifique-se de copiar todos os recursos necessários para este local antes de iniciar o servidor.

Para o start Tomcat e o servidor de licenças, execute `catalina.bat start` do diretório [!DNL bin] do Tomcat.
