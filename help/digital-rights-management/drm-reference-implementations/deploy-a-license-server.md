---
title: Implantar o servidor de licenças
description: Implantar o servidor de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Implantar o servidor de licença{#deploy-the-license-server}

1. Copie seus arquivos war de implementação de referência para o diretório `webapps` no servidor Tomcat.

   Para usar o servidor de licença de implementação de referência como está, basta copiar o arquivo WAR do servidor de licenças ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) para o diretório `webapps` no seu servidor Tomcat.

   Se estiver personalizando o servidor de licença de implementação de referência, copie os arquivos war do servidor criados a partir de `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` para o diretório `webapps`.

   >[!NOTE]
   >
   >Se você implantou anteriormente os arquivos WAR do servidor de licenças, talvez seja necessário excluir os diretórios WAR descompactados no diretório [!DNL webapps] no servidor Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Não implante [!DNL edsws.war] a menos que você exija compatibilidade com o conteúdo do Flash Media Rights Management (FMRMS) v1.5. (Esse é um requisito muito raro.)
   >
   >Se preferir impedir que o Tomcat desempache arquivos WAR, edite `server.xml` no diretório `conf` e defina `unpackWARs` para `false`.

1. Copie todo o conteúdo do diretório `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` no diretório [!DNL tomcat].

   O diretório [!DNL resources] inclui:

   * [!DNL flashaccesstools.properties] - O arquivo de propriedades do servidor de licenças.
   * [!DNL log4j.xml] - Configuração de registro do servidor de licenças
   * [!DNL *.pol] - Arquivos de política DRM de exemplo.

   Além disso, você também pode optar por copiar os arquivos de certificação do Adobe para esse local.

1. Modifique as configurações do servidor de licença em [!DNL flashaccesstools.properties] para refletir a configuração do servidor.

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

1. Edite o arquivo `catalina.properties` no diretório Tomcat `conf`; adicione o local do diretório [!DNL resources] (ou o local alternativo em que você armazenou seu arquivo de propriedades e outros arquivos de recursos) à propriedade `shared.loader`.

   Por exemplo, se você tiver `flashaccess-refimpl.properties` localizado em [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Isso coloca `flashaccess-refimpl.properties` no classpath.
1. Certifique-se de que os outros arquivos de recurso ( [!DNL log4j.xml], arquivos de política, certificações) estejam no diretório [!DNL resources] ou estejam no classpath e no local especificado em [!DNL flashaccess-refimpl.properties].

   Você provavelmente desejará executar inicialmente `log4j` no modo de depuração. Em [!DNL log4j.xml], defina `debug` como verdadeiro:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. No diretório Tomcat [!DNL bin], inicie o servidor.

   No Linux:

   ```
   catalina.sh start
   ```

   No Windows:

   ```
   catalina.bat start
   ```
