---
title: Encadeamento de licença aprimorado
description: Encadeamento de licença aprimorado
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Encadeamento de licença aprimorado {#enhanced-license-chaining}

Com o encadeamento de licença aprimorado no Adobe Access 3.0, é recomendável emitir uma Folha e uma Raiz na primeira vez que o usuário solicita uma licença para uma máquina específica. Se o usuário já tiver a licença Raiz, o servidor poderá emitir apenas uma Folha (chame `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar se o cliente já tem uma Raiz 3.0 Avançada). Para solicitações de licença subsequentes, o cliente indicará que já tem uma Folha e uma Raiz, portanto, o servidor deve emitir uma nova licença de Raiz. Quando o encadeamento de licença aprimorado é usado, `setRootKeyRetrievalInfo()` deve ser chamado para fornecer as credenciais necessárias para descriptografar a chave de criptografia raiz na política.

>[!NOTE]
>
>Se a política suportar o 3.0 Enhanced License Chaining, mas o cliente for o Adobe Access 2.0, o servidor emitirá uma licença 2.0 encadeada original. Para determinar a versão do cliente, use LicenseRequestMessage.getClientVersion().

