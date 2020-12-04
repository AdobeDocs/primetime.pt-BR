---
seo-title: Configurar o SSL no servidor BEES
title: Configurar o SSL no servidor BEES
uuid: 041a106e-8b21-4018-815d-b7ea48c3de03
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Configure o SSL no servidor BEES {#configure-ssl-on-your-bees-server}

1. Forneça o certificado SSL do servidor para o contato do Adobe que forneceu este software.

   O certificado será adicionado como um certificado confiável ao armazenamento confiável DRM da Primetime Cloud.
1. Para habilitar a autenticação de cliente para a conexão SSL (desabilitada nesta versão):
   1. Adicione os certificados `[!DNL clouddrm-transport.cer]` e `[!DNL AdobeFlashAccessIntermediateCA.cer]` ao repositório confiável usado para autenticação de cliente.
   1. Ative a autenticação de cliente na sua configuração SSL.
