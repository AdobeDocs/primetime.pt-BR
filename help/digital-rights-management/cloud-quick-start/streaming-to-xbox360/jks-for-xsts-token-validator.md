---
seo-title: Criar JKS para um validador XSTS
title: Criar JKS para um validador XSTS
uuid: e02b517d-0b72-4e95-92b2-09b8f785cce6
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Criar JKS para um validador XSTS{#create-jks-for-an-xsts-validator}

1. Descubra o nome alias do certificado privado, localizado no arquivo parceiro [!DNL .pfx].

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Converta [!DNL .pfx] em [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (onde `<alias>` é o nome alias do certificado privado que você descobriu na Etapa 1.)
1. Importe [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Coloque [!DNL xsts.jks] em seu diretório inicial Tomcat e defina `-Dxsts-keystore-password=****` para Tomcat.

Se [!DNL xsts_partner_cert.pfx] e [!DNL xsts.jks] estiverem usando senhas diferentes, atualize a senha `xsts` em `jks` para torná-las iguais.

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
