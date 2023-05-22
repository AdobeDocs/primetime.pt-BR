---
title: Criar JKS para um validador XSTS
description: Criar JKS para um validador XSTS
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Criar JKS para um validador XSTS{#create-jks-for-an-xsts-validator}

1. Descubra o nome do alias do certificado privado, localizado no parceiro [!DNL .pfx] arquivo.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Converter [!DNL .pfx] para [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (onde `<alias>` é o nome de alias do certificado privado descoberto na Etapa 1.)
1. Importar [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] no diretório inicial do Tomcat e defina `-Dxsts-keystore-password=****` para Tomcat.

Se [!DNL xsts_partner_cert.pfx] e [!DNL xsts.jks] estiverem usando senhas diferentes, atualize o `xsts` senha em `jks` para torná-las iguais.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
