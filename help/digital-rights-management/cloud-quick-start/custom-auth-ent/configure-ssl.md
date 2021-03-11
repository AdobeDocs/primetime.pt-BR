---
title: Configurar SSL no servidor BEES
description: Configurar SSL no servidor BEES
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Configurar SSL no servidor BEES {#configure-ssl-on-your-bees-server}

1. Forneça o certificado SSL do servidor para o Adobe entre em contato com o fornecedor deste software.

   O certificado será adicionado como um certificado confiável ao armazenamento confiável DRM da Primetime Cloud.
1. Para habilitar a autenticação de cliente para a conexão SSL (desabilitada nesta versão):
   1. Adicione os certificados `[!DNL clouddrm-transport.cer]` e `[!DNL AdobeFlashAccessIntermediateCA.cer]` ao armazenamento confiável usado para autenticação de cliente.
   1. Ative a autenticação de cliente na sua configuração SSL.
