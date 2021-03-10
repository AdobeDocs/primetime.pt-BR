---
title: Configuração do HSM
description: Configuração do HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Configuração do HSM {#hsm-configuration}

Se você optar por usar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração [!DNL pkcs11.cfg]. Este arquivo deve estar localizado no diretório *LicenseServer.ConfigRoot*. Consulte o diretório [!DNL Adobe Access Server for Protected Streaming/configs] no DVD de acesso ao Adobe para obter um exemplo de arquivo de configuração PKCS11. Para obter informações sobre o formato de [!DNL pkcs11.cfg], consulte a documentação do provedor Sun PKCS11 .

Para verificar se o seu arquivo de configuração HSM e Sun PKCS11 está configurado corretamente, você pode usar o seguinte comando do diretório em que o arquivo [!DNL pkcs11.cfg] está localizado ( [!DNL keytool] está instalado com o Java JRE e o JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se você vir suas credenciais na lista, o HSM é configurado corretamente e o servidor de licenças poderá acessar as credenciais.

>[!NOTE]
>
>No momento, o servidor de acesso ao Adobe para transmissão protegida não suporta HSMs em SO Windows de 64 bits.
