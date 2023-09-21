---
title: Configurar e implantar o servidor para transmissão protegida
description: Configurar e implantar o servidor para transmissão protegida
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Configurar e implantar o servidor para transmissão protegida {#set-up-and-deploy-the-server-for-protected-streaming}

1. Defina a pasta de configuração no DVD do Primetime DRM:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copiar a amostra `configs` pasta para o seu `<Tomcat_installation_dir>` e renomear a pasta copiada para `licenseserver`.

   O caminho para a pasta de configurações agora deve ser `<Tomcat_install_dir>\licenseserver\`.
1. Executar `Scrambler.bat` para obter as senhas criptografadas para os arquivos PFX do servidor de transporte e licença no DRM do Primetime `<DVD>` `\Adobe Access Server for Protected Streaming\` diretório:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Copie os arquivos PFX para o `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` diretório.
1. Edite a configuração de locatário correspondente no `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, com as seguintes configurações:

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

1. Copie o `flashaccessserver.war` do CD para o `<TomcatInstallDir>\webapps\` diretório.
1. Se o Tomcat estiver em execução, interrompa a instância do Tomcat em execução pressionando `<CTRL-C>` na janela command (se tiver sido iniciado na janela command). Você também pode parar o servidor do aplicativo Serviços do Windows se o Tomcat tiver sido instalado como um Serviço do Windows.
1. Para iniciar o Tomcat, digite o seguinte comando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Para verificar a configuração, insira o seguinte URL em um navegador:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
