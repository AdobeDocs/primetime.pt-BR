---
title: Configuração de HSM
description: Configuração de HSM
copied-description: true
exl-id: a3e5759e-1419-4519-bcd7-de83364a48f8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Configuração de HSM {#hsm-configuration}

Se optar por usar um HSM para armazenar suas credenciais de servidor, você deverá carregar as chaves privadas e os certificados no HSM e criar um [!DNL pkcs11.cfg] arquivo de configuração. Esse arquivo deve estar localizado no *LicenseServer.ConfigRoot* diretório. Consulte a [!DNL Adobe Access Server for Protected Streaming/configs] no DVD de Acesso ao Adobe para obter um exemplo de arquivo de configuração PKCS11. Para obter informações sobre o formato de [!DNL pkcs11.cfg], consulte a documentação do provedor Sun PKCS11.

Para verificar se o arquivo de configuração HSM e Sun PKCS11 está configurado corretamente, você pode usar o seguinte comando do diretório onde o [!DNL pkcs11.cfg] o arquivo está localizado ( [!DNL keytool] O é instalado com o Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se você vir suas credenciais na lista, o HSM é configurado corretamente e o servidor de licença poderá acessar as credenciais.

>[!NOTE]
>
>No momento, o Adobe Access Server para Streaming protegido não oferece suporte a HSMs em SOs Windows de 64 bits.
