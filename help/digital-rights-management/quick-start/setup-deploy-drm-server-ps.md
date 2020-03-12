---
seo-title: Configurar e implantar o servidor para o Protected Streaming
title: Configurar e implantar o servidor para o Protected Streaming
uuid: 300a1b63-0bf0-48a8-977d-212563025c19
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Configurar e implantar o servidor para o Protected Streaming {#set-up-and-deploy-the-server-for-protected-streaming}

1. Configure a pasta de configuração no DVD DRM Primetime:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copie a `configs` pasta de amostra para sua pasta `<Tomcat_installation_dir>` e renomeie a pasta copiada para `licenseserver`.

   O caminho para a pasta de configurações agora deve ser `<Tomcat_install_dir>\licenseserver\`.
1. Execute `Scrambler.bat` para obter as senhas criptografadas para os arquivos PFX do servidor de transporte e licença no diretório DRM `<DVD>` `\Adobe Access Server for Protected Streaming\` Primetime:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Copie os arquivos PFX para o `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` diretório.
1. Edite a configuração de locatário correspondente em `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, com as seguintes configurações:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. Execute o `Validator.bat` utilitário para verificar se a configuração é válida:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Copie o `flashaccessserver.war` arquivo do CD para o `<TomcatInstallDir>\webapps\` diretório.
1. Se Tomcat estiver em execução, pare a instância Tomcat em execução pressionando `<CTRL-C>` na janela de comando (se ela foi iniciada a partir da janela de comando). Você também pode interromper o servidor do aplicativo Windows Services se o Tomcat tiver sido instalado como um Serviço do Windows.
1. Para iniciar o Tomcat, digite o seguinte comando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Para verificar a configuração, insira o seguinte URL em um navegador:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
