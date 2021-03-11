---
description: O servidor de implementação de referência pode ajudá-lo a criar um servidor de licença totalmente funcional que use todos os recursos do SDK Java do Adobe Primetime DRM.
title: Servidor de licenças
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Servidor de licenças {#license-server}

O servidor de implementação de referência pode ajudá-lo a criar um servidor de licença totalmente funcional que use todos os recursos do SDK Java do Adobe Primetime DRM.

Nesta implementação, os usuários são autenticados com base nas entradas do usuário em um banco de dados. O servidor inclui lógica comercial de demonstração para a emissão de licenças e fornece suporte de compatibilidade para o Flash Media Rights Management Server 1.0 e 1.5.

## Requisitos do servidor de licenças {#license-server-requirements}

Requisitos do servidor de licenças:

* Instale o Tomcat 6.0 ou posterior
* Instale um banco de dados, por exemplo, MySQL (disponível no DVD, em [!DNL Third Party\MySQL])
* Verifique se o Java 1.6 ou posterior está instalado
* Para executar scripts de criação de amostra, verifique se você tem Ant 1.8 ou posterior

Depois de instalar o Tomcat e o MySQL, entre em contato com o Adobe para obter o conjunto de credenciais de DRM necessárias.

## Criar o servidor de licenças {#build-the-license-server}

>[!NOTE]
>
>A criação do servidor de licenças só é necessária se você pretende modificar o código-fonte. Para fins de avaliação, você pode simplesmente usar os arquivos WAR conforme enviados.

O servidor de licenças de implementação de referência inclui todo o código fonte do servidor de licenças ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), juntamente com um script de compilação Ant ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) com o qual você pode personalizar o servidor de licenças para atender às suas necessidades comerciais.

1. Modifique o script de compilação Ant para especificar os locais de seu SDK de DRM Primetime, Tomcat, MySQL e Log4J.

   Abra o arquivo [!DNL build-refimpl.xml] em um editor de texto e defina estes valores de propriedade:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Execute o script de build Ant com a propriedade `all` no diretório onde o script de build Ant está localizado.

   ```
   ant -f build-refimpl.xml all
   ```

   O script de criação Ant cria um diretório [!DNL refimpl-build/wars] que inclui os arquivos WAR do servidor.
