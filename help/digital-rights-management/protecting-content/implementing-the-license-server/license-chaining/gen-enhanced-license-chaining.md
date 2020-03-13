---
seo-title: Encadeamento de licença aprimorado
title: Encadeamento de licença aprimorado
uuid: f869b4e7-4b24-4832-94a7-b7143567ab58
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Encadeamento de licença aprimorado {#enhanced-license-chaining}

Se uma política de DRM for usada para gerar uma licença que suporte encadeamento de licença, o servidor deverá decidir se deseja emitir uma licença Leaf, uma licença Root ou ambos. Se quiser determinar que tipo de licença uma política de DRM suporta, você deve usar `Policy.getLicenseChainType()`ou chamar `Policy.getRootLicenseId()` para determinar se a política de DRM tem uma licença raiz. Com o encadeamento de licença do Adobe Primetime DRM 2.0, o servidor geralmente emite uma licença em folha na primeira vez que um usuário solicita uma licença para uma máquina específica e uma licença raiz posteriormente. Se você quiser determinar se o computador já tem uma licença de folha para a política especificada, é necessário ligar para `LicenseRequestMessage.clientHasLeafForPolicy()`.

Com o encadeamento aprimorado de licença no Adobe Primetime DRM 3.0, recomenda-se a emissão de uma Leaf e uma Root na primeira vez que o usuário solicita uma licença para uma máquina específica. Se o usuário já tiver a licença Raiz, o servidor poderá emitir apenas uma Folha (chame `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar se o cliente já tem uma Raiz 3.0 Avançada). Para solicitações de licença subsequentes, o cliente indica que já tem uma Leaf e uma Raiz, portanto, o servidor deve emitir uma nova licença de Raiz. Quando o encadeamento de licença aprimorado é usado, `setRootKeyRetrievalInfo()` deve ser chamado para fornecer as credenciais necessárias para descriptografar a chave de criptografia raiz na política de DRM.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>Se a política suportar o 3.0 Enhanced License Encadeamento, mas o cliente for Primetime DRM 2.0, o servidor emitirá uma licença encadeada original 2.0. Para determinar a versão do cliente, use `LicenseRequestMessage.getClientVersion()`.

