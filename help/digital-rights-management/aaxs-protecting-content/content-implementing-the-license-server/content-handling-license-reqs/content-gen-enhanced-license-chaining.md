---
seo-title: Encadeamento de licença aprimorado
title: Encadeamento de licença aprimorado
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: da8736769f7b47318dbd955aa854f83ae64d6d7b

---


# Encadeamento de licença aprimorado {#enhanced-license-chaining}

Com o encadeamento aprimorado de licença no Adobe Access 3.0, recomenda-se a emissão de uma Leaf e uma Root na primeira vez que o usuário solicita uma licença para uma máquina específica. Se o usuário já tiver a licença Raiz, o servidor poderá emitir apenas uma Folha (chame `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar se o cliente já tem uma Raiz 3.0 Avançada). Para solicitações de licença subsequentes, o cliente indicará que já tem uma Folha e uma Raiz, portanto, o servidor deve emitir uma nova licença de Raiz. Quando o encadeamento de licença aprimorado é usado, `setRootKeyRetrievalInfo()` deve ser chamado para fornecer as credenciais necessárias para descriptografar a chave de criptografia raiz na política.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Se a política suportar o Encadeamento de licenças aprimorado 3.0, mas o cliente for o Adobe Access 2.0, o servidor emitirá uma licença encadeada original 2.0. Para determinar a versão do cliente, use LicenseRequestMessage.getClientVersion().

