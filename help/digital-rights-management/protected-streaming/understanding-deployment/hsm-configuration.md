---
description: Se você selecionar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração pkcs11.cfg.
title: Configuração de HSM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Configuração de HSM{#hsm-configuration}

Se você selecionar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração pkcs11.cfg.

Você deve localizar o arquivo de configuração no *LicenseServer.ConfigRoot* diretório.

Consulte a [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] no DVD do Adobe Primetime DRM para obter um exemplo de arquivo de configuração PKCS11.

Consulte a documentação do provedor Sun PKCS11 sobre o formato de [!DNL pkcs11.cfg] arquivo.

Você pode usar o seguinte comando no diretório em que o [!DNL pkcs11.cfg] o arquivo está localizado ( [!DNL keytool] O é instalado com o Java JRE e JDK) para verificar se o arquivo de configuração HSM e Sun PKCS11 foi configurado corretamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se você conseguir exibir suas credenciais na lista, o HSM está configurado corretamente e o servidor de licença agora pode acessar as credenciais.
