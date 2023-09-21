---
title: Gerar uma solicitação de assinatura de certificado (Solicitante)
description: Gerar uma solicitação de assinatura de certificado (Solicitante)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Gerar uma solicitação de assinatura de certificado (Solicitante) {#generate-a-certificate-signing-request-requester}

1. Gere um par de chaves. Para usar um utilitário como OpenSSL, abra uma Janela de Comando e digite o seguinte:

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >A Adobe recomenda incluir o tipo de certificado (lic, pkgr, trans, trial ou eval) no nome da chave. Essa convenção de nomenclatura facilita a implantação no servidor de licenças. Este exemplo usa &quot;mycompany-license.key&quot;. Para as versões de Avaliação e Avaliação, use &quot;mycompany-eval.key&quot; e &quot;mycompany-trial.key&quot;.

1. Digite uma senha para proteger a chave privada.

   As senhas devem conter pelo menos 12 caracteres. Os caracteres devem incluir uma mistura de caracteres ASCII maiúsculos e minúsculos e números. Para usar o OpenSSL para gerar uma senha forte, abra uma Janela de Comando e digite o seguinte:

   ```
   openssl rand -base64 8
   ```

1. Gerar uma solicitação de assinatura de certificado (CSR).

   Para usar o OpenSSL para gerar uma CSR, abra uma Janela de Comando e insira o seguinte:

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. Você será solicitado a digitar a senha da chave privada.
1. Crie uma cópia de backup da sua chave privada e senha.

   Se você perder a chave privada ou se ela for comprometida, entre em contato com o Administrador de certificados de Adobe para revogar seu certificado e solicitar um novo.

   >[!NOTE]
   >
   >A Adobe recomenda o uso de um HSM para proteger sua chave privada e senha.
