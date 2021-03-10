---
title: Encadeamento de licença aprimorado
description: Encadeamento de licença aprimorado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Encadeamento de licença aprimorado {#enhanced-license-chaining}

Se uma política de DRM for usada para gerar uma licença que suporte o encadeamento de licenças, o servidor deverá decidir se deseja emitir uma licença de Folha, uma licença de Raiz ou ambos. Se quiser determinar o tipo de licença que uma política de DRM suporta, use `Policy.getLicenseChainType()` ou chame `Policy.getRootLicenseId()` para determinar se a política de DRM tem uma licença raiz. Com o encadeamento da licença do Adobe Primetime DRM 2.0, o servidor geralmente emite uma licença de folha na primeira vez que um usuário solicita uma licença para uma máquina específica e uma licença de raiz posteriormente. Se você quiser determinar se a máquina já tem uma licença de folha para a política especificada, é necessário chamar `LicenseRequestMessage.clientHasLeafForPolicy()`.

Com o encadeamento de licença aprimorado no Adobe Primetime DRM 3.0, é recomendável emitir uma Folha e uma Raiz na primeira vez que o usuário solicita uma licença para uma máquina específica. Se o usuário já tiver a licença Raiz, o servidor poderá emitir apenas uma Folha (chame `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar se o cliente já tem uma Raiz 3.0 Avançada). Para solicitações de licença subsequentes, o cliente indica que já tem uma Folha e uma Raiz, portanto, o servidor deve emitir uma nova licença de Raiz. Quando o encadeamento de licença aprimorado é usado, `setRootKeyRetrievalInfo()` deve ser chamado para fornecer as credenciais necessárias para descriptografar a chave de criptografia raiz na política de DRM.

>[!NOTE]
>
>Se a política suportar o 3.0 Enhanced License Chainting, mas o cliente for o Primetime DRM 2.0, o servidor emitirá uma licença 2.0 encadeada original. Para determinar a versão do cliente, use `LicenseRequestMessage.getClientVersion()`.

