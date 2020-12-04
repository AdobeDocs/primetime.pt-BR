---
seo-title: Gerar uma solicitação de assinatura de certificado (Solicitante)
title: Gerar uma solicitação de assinatura de certificado (Solicitante)
uuid: 04abd5d2-77ac-4f89-8bea-31d389159aee
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Gerar uma solicitação de assinatura de certificado (Solicitante) {#generate-a-certificate-signing-request-requester}

1. Gere um par de chaves. Para usar um utilitário como OpenSSL, abra uma Janela de comando e digite o seguinte:

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >A Adobe recomenda a inclusão do tipo de certificado (lic, pkgr, trans, versão de avaliação ou eval) no nome da chave. Essa convenção de nomenclatura facilita a implantação no servidor de licenças. Este exemplo usa &quot;mycompany-license.key&quot;. Para as versões de Avaliação e Avaliação, use &quot;mycompany-eval.key&quot; e &quot;mycompany-trial.key&quot;.

1. Digite uma senha para proteger a chave privada.

   As senhas devem conter pelo menos 12 caracteres. Os caracteres devem incluir uma mistura de caracteres ASCII maiúsculos e minúsculos. Para usar o OpenSSL para gerar uma senha forte, abra uma Janela de Comando e digite o seguinte:

   ```
   openssl rand -base64 8
   ```

1. Gerar uma solicitação de assinatura de certificado (CSR).

   Para usar o OpenSSL para gerar um CSR, abra uma Janela de Comando e insira o seguinte:

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. Você será solicitado a digitar a senha da chave privada.
1. Crie uma cópia de backup da sua chave privada e senha.

   Se você perder a chave privada ou se ela estiver comprometida, entre em contato com o Administrador de certificados do Adobe para revogar seu certificado e solicitar um novo.

   >[!NOTE]
   >
   >O Adobe recomenda usar um HSM para proteger sua chave privada e senha.

