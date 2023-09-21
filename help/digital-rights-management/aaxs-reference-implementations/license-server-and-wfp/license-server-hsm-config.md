---
title: Configuração de HSM
description: Configuração de HSM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Configuração de HSM {#hsm-configuration}

O uso de um HSM não é necessário, mas é recomendado. A implementação de referência pode ser configurada para usar o provedor Sun PKCS11 para suporte a HSM. Para usar uma credencial em um HSM, você deve criar um arquivo de configuração para o provedor Sun PKCS11. Consulte a documentação da Sun para obter detalhes. Para verificar se o arquivo de configuração HSM e Sun PKCS11 está configurado corretamente, você pode usar o seguinte comando (keytool é instalado com o Java JDK):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Se você vir suas credenciais na lista, o HSM é configurado corretamente.

>[!NOTE]
>
>A partir do Java 1.7, o Sun Java de 64 bits para Windows não suporta as interfaces PKCS11 que o DRM de acesso Adobe requer para se comunicar com dispositivos HSM. Se você planeja usar um HSM, use uma versão de 32 bits do Java ou use um JDK que suporte as interfaces PKCS11 completas.
