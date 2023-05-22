---
title: Encadeamento de licenças aprimorado
description: Encadeamento de licenças aprimorado
copied-description: true
exl-id: 4b07b29c-e739-4bf9-b464-0c82f68542d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Encadeamento de licenças aprimorado {#enhanced-license-chaining}

Se uma política DRM for usada para gerar uma licença que ofereça suporte ao encadeamento de licenças, o servidor deverá decidir se emitirá uma licença Leaf, uma licença Root ou ambas. Para determinar o tipo de encadeamento de licenças aceito por uma política DRM, é necessário usar `Policy.getLicenseChainType()`, ou chame `Policy.getRootLicenseId()` para determinar se a política DRM tem uma licença raiz. Com o encadeamento de licenças do Adobe Primetime DRM 2.0, o servidor normalmente emite uma licença folha na primeira vez que um usuário solicita uma licença para uma máquina específica e, posteriormente, uma licença raiz. Se você quiser determinar se a máquina já tem uma licença folha para a política especificada, será necessário chamar `LicenseRequestMessage.clientHasLeafForPolicy()`.

Com o encadeamento de licenças aprimorado no Adobe Primetime DRM 3.0, é recomendável emitir uma Folha e uma Raiz na primeira vez que o usuário solicitar uma licença para uma máquina específica. Se o usuário já tiver a licença Raiz, o servidor poderá emitir apenas uma Folha (chamada de `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar se o cliente já tem uma Raiz aprimorada 3.0). Para solicitações de licença subsequentes, o cliente indica que já tem uma Folha e uma Raiz, portanto, o servidor deve emitir uma nova licença Raiz. Quando o encadeamento de licenças aprimorado for usado, `setRootKeyRetrievalInfo()` deve ser chamado para fornecer as credenciais necessárias para descriptografar a chave de criptografia raiz na política DRM.

>[!NOTE]
>
>Se a política suportar o Encadeamento de licenças aprimorado 3.0, mas o cliente for o Primetime DRM 2.0, o servidor emitirá uma licença encadeada original 2.0. Para determinar a versão do cliente, use `LicenseRequestMessage.getClientVersion()`.
