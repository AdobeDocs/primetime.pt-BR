---
title: Solicitar um certificado (Solicitante)
description: Solicitar um certificado (Solicitante)
copied-description: true
exl-id: 290231ec-1146-4bfb-a449-b8ff85704197
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
