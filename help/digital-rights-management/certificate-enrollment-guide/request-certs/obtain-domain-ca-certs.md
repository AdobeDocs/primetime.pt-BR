---
title: Obter certificados de autoridade de certificação de domínio
description: Obter certificados de autoridade de certificação de domínio
copied-description: true
exl-id: cad233e0-41f7-4897-ab5f-d5a098c37306
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Obter certificados de autoridade de certificação de domínio{#obtain-domain-ca-certificates}

Ao contrário do License Server, Packager ou certificado de Transporte, o certificado de CA de domínio não é emitido pelo Adobe. Você pode obter esse certificado de uma autoridade de certificação ou gerar um certificado autoassinado para usar com essa finalidade.

O certificado CA de domínio deve usar uma chave de 1024 bits e conter os atributos padrão necessários em um certificado CA:

* Extensão de Restrições Básicas com o sinalizador CA definido como verdadeiro
* A extensão Uso de Chave que especifica Assinatura de Certificado é permitida

Por exemplo, usando o OpenSSL, um certificado CA autoassinado pode ser gerado da seguinte maneira:

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
