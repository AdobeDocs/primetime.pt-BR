---
description: Você pode configurar a implementação de referência com o provedor Sun PKCS#11 compatível com HSM. Embora a utilização de um HSM não seja obrigatória, é recomendável.
seo-description: Você pode configurar a implementação de referência com o provedor Sun PKCS#11 compatível com HSM. Embora a utilização de um HSM não seja obrigatória, é recomendável.
seo-title: Configuração do HSM
title: Configuração do HSM
uuid: 2741ac40-aa42-4aa7-9864-037f3ed3dee2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Configuração do HSM{#hsm-configuration}

Você pode configurar a implementação de referência com o provedor Sun PKCS#11 compatível com HSM. Embora a utilização de um HSM não seja obrigatória, é recomendável.

Para usar uma credencial em um HSM, você deve criar um arquivo de configuração para o provedor Sun PKCS#11. Para obter mais informações, consulte o Guia [de referência PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html)Java.

Para verificar se seu arquivo de configuração HSM e Sun PKCS#11 estão configurados, digite o seguinte comando usando a ferramenta de chave instalada com o Java JDK:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Você configurou o HSM corretamente se puder visualização suas credenciais na lista.

>[!NOTE]
>
>A partir do Java 1.7, o Sun Java para Windows de 64 bits não oferece mais suporte às interfaces PKCS#11 que o Adobe Primetime DRM exige para se comunicar com dispositivos HSM. Se você planeja usar um HSM, certifique-se de usar uma versão de 32 bits do Java ou um JDK que suporte as interfaces completas do PKCS#11.

