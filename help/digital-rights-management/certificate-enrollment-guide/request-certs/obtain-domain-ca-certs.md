---
title: Obter certificados de AC de Domínio
description: Obter certificados de AC de Domínio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Obter certificados de AC de Domínio{#obtain-domain-ca-certificates}

Ao contrário do License Server, do Packager ou do Certificado de Transporte, o certificado da autoridade de certificação de domínio não é emitido pelo Adobe. Você pode obter esse certificado de uma autoridade de certificação ou gerar um certificado autoassinado para uso com essa finalidade.

O certificado de autoridade de certificação de domínio deve usar uma chave de 1024 bits e conter os atributos padrão necessários em um certificado de autoridade de certificação:

* Extensão Restrições Básicas com o sinalizador CA definido como true
* A extensão de Uso de Chave que especifica a Assinatura de Certificado é permitida

Por exemplo, usando OpenSSL, um certificado CA autoassinado pode ser gerado da seguinte maneira:

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

