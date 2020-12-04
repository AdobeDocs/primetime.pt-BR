---
seo-title: Converter arquivos
title: Converter arquivos
uuid: e17ee003-5ac2-4bb8-83b7-81ee8fa9ee46
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Converter arquivos{#convert-files}

Usando um utilitário como OpenSSL e a chave privada, o Solicitante gera os arquivos PKCS#12 (pfx) e PEM/DER inserindo os seguintes comandos em uma Janela de comando:

1. Converta o arquivo PKCS#7 em um arquivo PEM temporário.

   Para usar o OpenSSL, abra uma Janela de Comando e insira o seguinte:

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >Este PEM temporário contém seu certificado e os certificados para CAs intermediárias. Use esses certificados para gerar o arquivo PFX.

1. Converta o arquivo PEM temporário em um arquivo PFX.

   Para usar o OpenSSL, abra uma Janela de Comando e insira o seguinte:

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. Converta o arquivo PEM temporário em um arquivo PEM final.

   Para usar o OpenSSL, abra uma Janela de Comando e insira o seguinte:

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >Embora não seja obrigatório, o Adobe recomenda o uso de senhas diferentes para a chave privada (private_key_password) e o PFX (pfx_password).

   Este arquivo PEM final contém apenas seu certificado.

1. Converta o arquivo PEM em um arquivo DER.

   Para usar o OpenSSL, abra uma Janela de Comando e insira o seguinte:

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >Os arquivos DER são necessários apenas para o empacotador de HTTP Dynamic Streaming.

