---
description: Se você selecionar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração pkcs11.cfg.
title: Configuração do HSM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Configuração do HSM{#hsm-configuration}

Se você selecionar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração pkcs11.cfg.

Você deve localizar o arquivo de configuração no diretório *LicenseServer.ConfigRoot*.

Consulte o diretório [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] no DVD DRM do Adobe Primetime para obter um exemplo de arquivo de configuração PKCS11.

Consulte a documentação do provedor Sun PKCS11 sobre o formato do arquivo [!DNL pkcs11.cfg].

Você pode usar o seguinte comando do diretório em que o arquivo [!DNL pkcs11.cfg] está localizado ( [!DNL keytool] está instalado com o JRE Java e o JDK) para verificar se o arquivo de configuração HSM e Sun PKCS11 foi configurado corretamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se você puder exibir suas credenciais na lista, o HSM será configurado corretamente e o servidor de licenças poderá acessar as credenciais.
