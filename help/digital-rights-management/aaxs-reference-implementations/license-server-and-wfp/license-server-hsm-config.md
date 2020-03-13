---
seo-title: Configuração do HSM
title: Configuração do HSM
uuid: 1cc5be99-c24c-4c1e-9348-fb69f96d8ca5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configuração do HSM {#hsm-configuration}

O uso de um HSM não é obrigatório, mas é recomendado. A implementação de referência pode ser configurada para usar o provedor Sun PKCS11 para suporte a HSM. Para usar uma credencial em um HSM, é necessário criar um arquivo de configuração para o provedor Sun PKCS11. Consulte a documentação do Sun para obter detalhes. Para verificar se seu arquivo de configuração HSM e Sun PKCS11 estão configurados corretamente, você pode usar o seguinte comando (keytool is installed with the Java JDK):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Se você vir suas credenciais na lista, o HSM será configurado corretamente.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>A partir do Java 1.7, o Sun Java para Windows de 64 bits não oferece suporte às interfaces PKCS11 que o Adobe Access DRM requer para se comunicar com dispositivos HSM. Se você planeja usar um HSM, use uma versão de 32 bits do Java ou um JDK que suporte as interfaces completas do PKCS11.

