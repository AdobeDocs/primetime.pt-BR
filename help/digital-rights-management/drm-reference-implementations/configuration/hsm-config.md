---
description: Você pode configurar a implementação de referência com o provedor Sun PKCS#11 compatível com HSM. Embora o uso de um HSM não seja obrigatório, ele é recomendado.
title: Configuração de HSM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Configuração de HSM{#hsm-configuration}

Você pode configurar a implementação de referência com o provedor Sun PKCS#11 compatível com HSM. Embora o uso de um HSM não seja obrigatório, ele é recomendado.

Para usar uma credencial em um HSM, você deve criar um arquivo de configuração para o provedor Sun PKCS#11. Para obter mais informações, consulte [Guia de referência do Java PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Para verificar se o arquivo de configuração HSM e Sun PKCS#11 está configurado, digite o seguinte comando usando a ferramenta de chave que foi instalada com o JDK do Java:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Você configurou o HSM corretamente se puder visualizar suas credenciais na lista.

>[!NOTE]
>
>Desde o Java 1.7, o Sun Java de 64 bits para Windows não é mais compatível com as interfaces PKCS#11 que o Adobe Primetime DRM exige para se comunicar com dispositivos HSM. Se você planeja usar um HSM, certifique-se de usar uma versão de 32 bits do Java ou usar um JDK que suporte as interfaces PKCS#11 completas.
