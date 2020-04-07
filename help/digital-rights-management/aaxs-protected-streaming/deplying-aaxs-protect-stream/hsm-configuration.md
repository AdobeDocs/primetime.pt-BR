---
seo-title: Configuração do HSM
title: Configuração do HSM
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: ac75f63f98060e1937570476362bb5d4458d1f85

---


# Configuração do HSM {#hsm-configuration}

Se você optar por usar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo [!DNL pkcs11.cfg] de configuração. Esse arquivo deve estar localizado no diretório *LicenseServer.ConfigRoot* . Consulte o [!DNL Adobe Access Server for Protected Streaming/configs] diretório no DVD do Adobe Access para obter um exemplo de arquivo de configuração PKCS11. Para obter informações sobre o formato de [!DNL pkcs11.cfg], consulte a documentação do provedor Sun PKCS11.

Para verificar se o arquivo de configuração HSM e Sun PKCS11 está configurado corretamente, você pode usar o seguinte comando do diretório onde o [!DNL pkcs11.cfg] arquivo está localizado ( [!DNL keytool] está instalado com o Java JRE e o JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se as credenciais forem exibidas na lista, o HSM será configurado corretamente e o servidor de licenças poderá acessá-las.

>[!NOTE]
>
>O Adobe Access Server for protected Streaming não suporta HSMs em SOs Windows de 64 bits.
