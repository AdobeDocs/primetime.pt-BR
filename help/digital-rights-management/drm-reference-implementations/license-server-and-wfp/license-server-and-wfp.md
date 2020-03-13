---
description: O servidor de implementação de referência pode ajudá-lo a criar um servidor de licenças totalmente funcional que use todos os recursos do Adobe Primetime DRM Java SDK.
seo-description: O servidor de implementação de referência pode ajudá-lo a criar um servidor de licenças totalmente funcional que use todos os recursos do Adobe Primetime DRM Java SDK.
seo-title: Servidor de licenças
title: Servidor de licenças
uuid: 39cb0d0f-f3dc-48e9-b6fd-6960a9ade291
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# Servidor de licenças {#license-server}

O servidor de implementação de referência pode ajudá-lo a criar um servidor de licenças totalmente funcional que use todos os recursos do Adobe Primetime DRM Java SDK.

Nesta implementação, os usuários são autenticados com base em entradas de usuários em um banco de dados. O servidor inclui lógica comercial de demonstração para a emissão de licenças e oferece suporte de compatibilidade para o Flash Media Rights Management Server 1.0 e 1.5.

## Requisitos do servidor de licenças {#license-server-requirements}

Requisitos do servidor de licenças:

* Instale o Tomcat 6.0 ou posterior
* Instale um banco de dados, por exemplo, MySQL (disponível no DVD, em [!DNL Third Party\MySQL])
* Verifique se o Java 1.6 ou posterior está instalado
* Para executar scripts de criação de amostra, verifique se você tem Ant 1.8 ou posterior

Depois de instalar o Tomcat e o MySQL, entre em contato com a Adobe para obter o conjunto de credenciais de DRM necessárias.

## Criar o servidor de licenças {#build-the-license-server}

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A criação do servidor de licenças só é necessária se você pretende modificar o código fonte. Para fins de avaliação, basta usar os arquivos WAR conforme enviados.

O servidor de licença de implementação de referência inclui todo o código fonte do servidor de licenças ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), juntamente com um script de compilação Ant ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) com o qual você pode personalizar o servidor de licenças para atender às suas necessidades comerciais.

1. Modifique o script de compilação Ant para especificar os locais do SDK do Primetime DRM, Tomcat, MySQL e Log4J.

   Abra o [!DNL build-refimpl.xml] arquivo em um editor de texto e defina estes valores de propriedade:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Execute o script de construção Ant com a `all` propriedade, no diretório em que o script de construção Ant está localizado.

   ```
   ant -f build-refimpl.xml all
   ```

   O script de criação Ant cria um [!DNL refimpl-build/wars] diretório que inclui os arquivos WAR do servidor.
