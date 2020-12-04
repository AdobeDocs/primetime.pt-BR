---
description: nulo
seo-description: nulo
seo-title: Implantar o servidor de licenças
title: Implantar o servidor de licenças
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Implantar o servidor de licenças{#deploy-the-license-server}

1. Copie seus arquivos de referência de implementação de guerra para o diretório `webapps` no servidor Tomcat.

   Para usar o servidor de licença de implementação de referência como está, basta copiar o arquivo WAR do servidor de licenças ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) para o diretório `webapps` no servidor Tomcat.

   Se você estiver personalizando o servidor de licenças de implementação de referência, copie os arquivos de guerra do servidor criados de `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` para o diretório `webapps`.

   >[!NOTE]
   >
   >Se você implantou anteriormente arquivos WAR do servidor de licenças, talvez seja necessário excluir os diretórios WAR descompactados no diretório [!DNL webapps] no servidor Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Não implante [!DNL edsws.war] a menos que você exija compatibilidade com versões anteriores do conteúdo do Rights Management de mídia de Flash (FMRMS) v1.5. (Este é um requisito muito raro.)
   >
   >Se você preferir impedir que o Tomcat desempacote arquivos WAR, edite `server.xml` no diretório `conf` e defina `unpackWARs` como `false`.

1. Copie todo o conteúdo do diretório `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` para o diretório [!DNL tomcat].

   O diretório [!DNL resources] inclui:

   * [!DNL flashaccesstools.properties] - O arquivo de propriedades do servidor de licenças.
   * [!DNL log4j.xml] - Configuração de registro do servidor de licenças
   * [!DNL *.pol] - Arquivos de política DRM de amostra.

   Além disso, você também pode optar por copiar os arquivos de certificação do Adobe para esse local.

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

1. Edite o arquivo `catalina.properties` no diretório Tomcat `conf`; adicione o local do diretório [!DNL resources] (ou o local alternativo onde você armazenou o arquivo de propriedades e outros arquivos de recursos) à propriedade `shared.loader`.

   Por exemplo, se você tem `flashaccess-refimpl.properties` localizado em [!DNL [home do Tomcat]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Isso coloca `flashaccess-refimpl.properties` no classpath.
1. Certifique-se de que seus outros arquivos de recurso ( [!DNL log4j.xml], arquivos de política, certificações) estejam no diretório [!DNL resources] ou no classpath e em seu local especificado em [!DNL flashaccess-refimpl.properties].

   Provavelmente, você desejará executar `log4j` inicialmente no modo de depuração. Em [!DNL log4j.xml], defina `debug` como verdadeiro:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. No diretório Tomcat [!DNL bin], start seu servidor.

   No Linux:

   ```
   catalina.sh start
   ```

   No Windows:

   ```
   catalina.bat start
   ```
