---
description: Você pode configurar a implementação de referência com o provedor Sun PKCS#11 compatível com HSM. Embora o uso de um HSM não seja obrigatório, ele é recomendado.
title: Configuração de HSM
exl-id: 87a7d242-8202-4749-91a6-e6697be6a61d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
