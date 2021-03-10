---
title: Configuração do HSM
description: Configuração do HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Configuração do HSM {#hsm-configuration}

Não é necessário usar um HSM, mas é recomendado. A implementação de referência pode ser configurada para usar o provedor Sun PKCS11 para suporte a HSM. Para usar uma credencial em um HSM, você deve criar um arquivo de configuração para o provedor Sun PKCS11. Consulte a documentação da Sun para obter detalhes. Para verificar se o seu arquivo de configuração HSM e Sun PKCS11 estão configurados corretamente, você pode usar o seguinte comando (keytool está instalado com o Java JDK):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Se você vir suas credenciais na lista, o HSM é configurado corretamente.

>[!NOTE]
>
>A partir do Java 1.7, o Sun Java para Windows de 64 bits não é compatível com as interfaces PKCS11 que o DRM de acesso ao Adobe requer para se comunicar com dispositivos HSM. Se você planeja usar um HSM, use uma versão de 32 bits do Java ou um JDK que seja compatível com todas as interfaces PKCS11.

