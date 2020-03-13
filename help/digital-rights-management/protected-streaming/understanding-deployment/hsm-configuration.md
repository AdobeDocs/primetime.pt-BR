---
description: Se você selecionar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração pkcs11.cfg.
seo-description: Se você selecionar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração pkcs11.cfg.
seo-title: Configuração do HSM
title: Configuração do HSM
uuid: 3610840b-082e-4a73-8aa5-5065f9232e0b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configuração do HSM{#hsm-configuration}

Se você selecionar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração pkcs11.cfg.

Você deve localizar o arquivo de configuração no diretório *LicenseServer.ConfigRoot* .

Consulte o [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] diretório no DVD DRM do Adobe Primetime para ver um exemplo de arquivo de configuração PKCS11.

Consulte a documentação do provedor Sun PKCS11 relativa ao formato do [!DNL pkcs11.cfg] arquivo.

Você pode usar o seguinte comando do diretório em que o [!DNL pkcs11.cfg] arquivo está localizado ( [!DNL keytool] está instalado com o Java JRE e o JDK) para verificar se o arquivo de configuração HSM e Sun PKCS11 foi configurado corretamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se você puder exibir suas credenciais na lista, o HSM está configurado corretamente e o servidor de licenças agora pode acessar as credenciais.
