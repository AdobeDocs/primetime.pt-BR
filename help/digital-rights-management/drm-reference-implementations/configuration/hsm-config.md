---
description: Você pode configurar a implementação de referência com o provedor Sun PKCS#11 que suporta HSM. Embora a utilização de um HSM não seja necessária, é recomendável.
title: Configuração do HSM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Configuração do HSM{#hsm-configuration}

Você pode configurar a implementação de referência com o provedor Sun PKCS#11 que suporta HSM. Embora a utilização de um HSM não seja necessária, é recomendável.

Para usar uma credencial em um HSM, você deve criar um arquivo de configuração para o provedor Sun PKCS#11. Para obter mais informações, consulte o [Guia de Referência do Java PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Para verificar se o seu arquivo de configuração HSM e Sun PKCS#11 está configurado, digite o seguinte comando usando a ferramenta de chave que foi instalada com o Java JDK:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Você configurou o HSM corretamente se puder exibir suas credenciais na lista.

>[!NOTE]
>
>Desde o Java 1.7, o Sun Java para Windows de 64 bits não é mais compatível com as interfaces PKCS#11 que o Adobe Primetime DRM requer para se comunicar com dispositivos HSM. Se você planeja usar um HSM, certifique-se de usar uma versão de 32 bits do Java ou um JDK que seja compatível com todas as interfaces PKCS#11.

