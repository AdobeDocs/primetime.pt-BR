---
title: Configurar SSL no servidor BEES
description: Configurar SSL no servidor BEES
copied-description: true
exl-id: 6823a71c-3be6-4c07-a3e6-e16bd931deaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Configurar SSL no servidor BEES {#configure-ssl-on-your-bees-server}

1. Forneça o certificado SSL do servidor ao contato do Adobe que forneceu o software.

   O certificado será adicionado como um certificado confiável ao armazenamento de confiança DRM da Primetime Cloud.
1. Para habilitar a autenticação de cliente para a conexão SSL (desabilitada nesta versão):
   1. Adicione o `[!DNL clouddrm-transport.cer]` e `[!DNL AdobeFlashAccessIntermediateCA.cer]` certificados para o armazenamento de confiança usado para autenticação de cliente.
   1. Habilite a autenticação do cliente na configuração do SSL.
