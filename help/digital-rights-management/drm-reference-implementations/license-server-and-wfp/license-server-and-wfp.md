---
description: O servidor de implementação de referência pode ajudar você a criar um servidor de licença totalmente funcional que use todos os recursos do SDK Java do Adobe Primetime DRM.
title: Servidor de licenças
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Servidor de licenças {#license-server}

O servidor de implementação de referência pode ajudar você a criar um servidor de licença totalmente funcional que use todos os recursos do SDK Java do Adobe Primetime DRM.

Nesta implementação, os usuários são autenticados com base nas entradas do usuário em um banco de dados. O servidor inclui lógica comercial de demonstração para emissão de licenças e oferece suporte de compatibilidade para o Flash Media Rights Management Server 1.0 e 1.5.

## Requisitos do servidor de licenças {#license-server-requirements}

Requisitos do servidor de licenças:

* Instalar Tomcat 6.0 ou posterior
* Instalar um banco de dados, por exemplo, MySQL (disponível no DVD, em [!DNL Third Party\MySQL])
* Verifique se o Java 1.6 ou posterior está instalado
* Para executar os scripts de construção de amostra, certifique-se de ter o Ant 1.8 ou posterior

Depois de instalar o Tomcat e o MySQL, entre em contato com o Adobe para obter o conjunto de credenciais de DRM necessárias.

## Criar o servidor de licenças {#build-the-license-server}

>[!NOTE]
>
>A criação do servidor de licenças só será necessária se você pretender modificar o código-fonte. Para fins de avaliação, você pode simplesmente usar os arquivos WAR conforme foram enviados.

O servidor de licenças de implementação de referência inclui todo o código-fonte do servidor de licenças ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), juntamente com um script de construção Ant ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) com o qual você pode personalizar o servidor de licenças para atender às suas necessidades comerciais.

1. Modifique o script de construção Ant para especificar a localização do SDK do Primetime DRM, Tomcat, MySQL e Log4J.

   Abra o [!DNL build-refimpl.xml] em um editor de texto e defina esses valores de propriedade:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Execute o script de construção Ant com o `all` propriedade, no diretório onde o script de construção Ant está localizado.

   ```
   ant -f build-refimpl.xml all
   ```

   O script de construção Ant cria um [!DNL refimpl-build/wars] diretório que inclui os arquivos WAR do servidor.
