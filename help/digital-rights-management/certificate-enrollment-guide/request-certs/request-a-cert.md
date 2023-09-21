---
title: Solicitar um certificado (Solicitante)
description: Solicitar um certificado (Solicitante)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Solicitar um certificado (Solicitante){#request-a-certificate-requester}

1. Faça logon no site de Registro de Certificado.

   O usuário que solicita um certificado deve ser um Solicitante.

1. Na guia Solicitação, selecione o tipo de certificado (License Server, Packager ou Transporte).

   >[!NOTE]
   >
   >Essa opção não é mostrada para as versões de Avaliação e Avaliação do SDK. Essas versões do SDK usam um certificado.

1. Siga um destes procedimentos:

   * Faça upload do arquivo CSR.
   * Copie as informações da CSR e cole-as no formulário.

     >[!NOTE]
     >
     >Para copiar as informações da CSR, selecione o texto entre, sem incluir, a tag inicial `(-----BEGIN CERTIFICATE REQUEST-----)` e marca de fim `(-----END CERTIFICATE REQUEST-----)`.

1. Clique em **[!UICONTROL Submit Request]** botão.

   Um email é enviado à Conta e aos Administradores Secundários para análise. O Solicitante tem Cc.
