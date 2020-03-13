---
description: nulo
seo-description: nulo
seo-title: Implantar o servidor de licenças
title: Implantar o servidor de licenças
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 29149594c4b41956a091ef27093304e74ff15f2f

---


# Implantar o servidor de licenças{#deploy-the-license-server}

1. Copie seus arquivos de referência de implementação de guerra para o `webapps` diretório no servidor Tomcat.

   Para usar o servidor de licença de implementação de referência como está, basta copiar o arquivo WAR do servidor de licenças ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) para o diretório no `webapps` servidor Tomcat.

   Se você estiver personalizando o servidor de licença de implementação de referência, copie os arquivos de guerra do servidor que você criou `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` para o `webapps` diretório.

   >[!NOTE]
   >
   >Se você implantou anteriormente arquivos WAR do servidor de licenças, talvez seja necessário excluir os diretórios WAR descompactados no [!DNL webapps] diretório do servidor Tomcat:        >
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Não implante [!DNL edsws.war] a menos que você exija compatibilidade com versões anteriores do conteúdo do Flash Media Rights Management (FMRMS) v1.5. (Este é um requisito muito raro.)
   >
   >Se você preferir impedir que o Tomcat desempacote arquivos WAR, edite `server.xml` no `conf` diretório e defina `unpackWARs` como `false`.

1. Copie todo o conteúdo do `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` diretório para dentro do seu [!DNL tomcat] diretório.

   O [!DNL resources] diretório inclui:

   * [!DNL flashaccesstools.properties] - O arquivo de propriedades do servidor de licenças.
   * [!DNL log4j.xml] - Configuração de registro do servidor de licenças
   * [!DNL *.pol] - Arquivos de política DRM de amostra.
   Além disso, você também pode optar por copiar os arquivos de certificação da Adobe para este local.

1. Modifique as configurações do servidor de licenças em [!DNL flashaccesstools.properties] para refletir a configuração do servidor.

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

1. Edite o `catalina.properties` arquivo em seu `conf` diretório Tomcat; adicione o local do seu [!DNL resources] diretório (ou o local alternativo onde você armazenou seu arquivo de propriedades e outros arquivos de recursos) à `shared.loader` propriedade.

   Por exemplo, se você tiver `flashaccess-refimpl.properties` localizado em [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Isso coloca `flashaccess-refimpl.properties` no classpath.
1. Certifique-se de que seus outros arquivos de recurso ( [!DNL log4j.xml], arquivos de política, certificações) estejam no [!DNL resources] diretório ou no classpath e na localização especificada em [!DNL flashaccess-refimpl.properties].

   Provavelmente, você desejará executar inicialmente `log4j` no modo de depuração. Em [!DNL log4j.xml], defina `debug` como true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. No [!DNL bin] diretório Tomcat, inicie o servidor.

   No Linux:

   ```
   catalina.sh start
   ```

   No Windows:

   ```
   catalina.bat start
   ```
