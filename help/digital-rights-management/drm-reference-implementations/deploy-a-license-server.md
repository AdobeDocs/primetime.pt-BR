---
title: Implantar o servidor de licenças
description: Implantar o servidor de licenças
copied-description: true
exl-id: 1439a5b2-eccb-41b7-a4d3-0673e727fb13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Implantar o servidor de licenças{#deploy-the-license-server}

1. Copie os arquivos WAR da implementação de referência para o `webapps` no servidor Tomcat.

   Para usar o servidor de licenças de implementação de referência como está, você pode simplesmente copiar o arquivo WAR do servidor de licenças ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) para o `webapps` no servidor Tomcat.

   Se você estiver personalizando o servidor de licenças de implementação de referência, copie os arquivos WAR do servidor criados a partir do `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` para o `webapps` diretório.

   >[!NOTE]
   >
   >Se você implantou anteriormente arquivos WAR do servidor de licenças, talvez precise excluir os diretórios WAR desempacotados na [!DNL webapps] no servidor Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Não implantar [!DNL edsws.war] a menos que você exija compatibilidade com versões anteriores do Flash Media Rights Management (FMRMS) v1.5. (Este é um requisito muito raro.)
   >
   >Se preferir impedir que o Tomcat descompacte arquivos WAR, edite `server.xml` no `conf` diretório e definir `unpackWARs` para `false`.

1. Copie todo o conteúdo do `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` diretório em seu [!DNL tomcat] diretório.

   A variável [!DNL resources] o diretório inclui:

   * [!DNL flashaccesstools.properties] - O arquivo de propriedades do servidor de licenças.
   * [!DNL log4j.xml] - Configuração de registro do servidor de licenças
   * [!DNL *.pol] - Arquivos de política DRM de exemplo.

   Além disso, você também pode optar por copiar os arquivos de certificação de Adobe para esse local.

1. Modificar configurações do servidor de licenças no [!DNL flashaccesstools.properties] para refletir a configuração do servidor.

   No mínimo, defina valores para as seguintes propriedades:

   * `config.resourcesDirectory`
   * `HandlerConfiguration.ServerTransportCredential`
   * `HandlerConfiguration.ServerTransportCredential.password`
   * `LicenseHandler.ServerCredential`
   * `LicenseHandler.ServerCredential.password`
   * `MetaDataConverter.SignatureParameters.ServerCredential`
   * `MetaDataConverter.SignatureParameters.ServerCredential.password`
   * `V2KeyParameters.LicenseServerUrl`
   * `V2KeyParameters.KeyOptions.AsymmetricKeyOptions.Certificate`
   * V2KeyParameters.LicenseServerTransportCertificate

1. Edite o `catalina.properties` arquivo no seu Tomcat `conf` diretório; adicione a localização do seu [!DNL resources] (ou o local alternativo onde você armazenou o arquivo de propriedades e outros arquivos de recursos) na `shared.loader` propriedade.

   Por exemplo, se você tiver `flashaccess-refimpl.properties` localizado em [!DNL [Início: Tomcat]\recursos\]:

   ```
   shared.loader=..\resources
   ```

   Este lugar `flashaccess-refimpl.properties` no classpath.
1. Verifique se os outros arquivos de recurso ( [!DNL log4j.xml], arquivos de política, certificações) estão na [!DNL resources] ou estão no classpath e sua localização especificada em [!DNL flashaccess-refimpl.properties].

   É provável que você queira executar inicialmente `log4j` no modo de depuração. Entrada [!DNL log4j.xml], definir `debug` para verdadeiro:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Do Tomcat [!DNL bin] diretório, inicie o servidor.

   No Linux:

   ```
   catalina.sh start
   ```

   No Windows:

   ```
   catalina.bat start
   ```
