---
title: Configurar e implantar o servidor para transmissão protegida
description: Configurar e implantar o servidor para transmissão protegida
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Configurar e implantar o servidor para transmissão protegida {#set-up-and-deploy-the-server-for-protected-streaming}

1. Configure a pasta de configuração no DVD DRM do Primetime:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copie a pasta `configs` de amostra para seu `<Tomcat_installation_dir>` e renomeie a pasta copiada para `licenseserver`.

   O caminho para a pasta de configurações agora deve ser `<Tomcat_install_dir>\licenseserver\`.
1. Execute `Scrambler.bat` para obter as senhas criptografadas para os arquivos PFX do servidor de transporte e licença no diretório Primetime DRM `<DVD>` `\Adobe Access Server for Protected Streaming\`:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Copie os arquivos PFX para o diretório `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\`.
1. Edite a configuração do locatário correspondente em `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, com as seguintes configurações:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. Execute o utilitário `Validator.bat` para verificar se a configuração é válida:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Copie o arquivo `flashaccessserver.war` do CD para o diretório `<TomcatInstallDir>\webapps\`.
1. Se Tomcat estiver em execução, pare a instância Tomcat em execução pressionando `<CTRL-C>` na janela de comando (se ela tiver sido iniciada a partir da janela de comando). Você também pode interromper o servidor do aplicativo Windows Services se o Tomcat tiver sido instalado como um Windows Service.
1. Para iniciar o Tomcat, digite o seguinte comando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Para verificar a configuração, insira o seguinte URL em um navegador:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
