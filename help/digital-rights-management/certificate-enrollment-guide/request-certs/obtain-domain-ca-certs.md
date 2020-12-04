---
seo-title: Obter certificados de AC de domínio
title: Obter certificados de AC de domínio
uuid: 41bbe02b-363a-47f4-9cc0-350730b6c787
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Obter certificados de AC de domínio{#obtain-domain-ca-certificates}

Ao contrário do certificado de Servidor de Licença, Packager ou Transport, o certificado de CA de Domínio não é emitido pelo Adobe. Você pode obter esse certificado de uma autoridade de certificação ou gerar um certificado autoassinado para usar para essa finalidade.

O certificado da CA de domínio deve usar uma chave de 1024 bits e conter os atributos padrão necessários em um certificado da CA:

* Extensão Restrições básicas com sinalizador CA definido como true
* A extensão de uso de chave que especifica a Assinatura de certificado é permitida

Por exemplo, usando o OpenSSL, um certificado CA autoassinado pode ser gerado da seguinte forma:

1. Crie um arquivo chamado [!DNL ca-extensions.txt] contendo:

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. Gerar chave:

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. Gerar CSR:

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. Gerar certificado:

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. Gerar senha:

   ```
   openssl rand -base64 8 
   ```

1. Gerar PFX:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```

