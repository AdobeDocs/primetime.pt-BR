---
title: Encadeamento de licenças aprimorado
description: Encadeamento de licenças aprimorado
copied-description: true
exl-id: 4548cdc4-4a55-411b-ad22-8c77927f4564
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Encadeamento de licenças aprimorado {#enhanced-license-chaining}

Com o aprimoramento do encadeamento de licenças no Adobe Access 3.0, é recomendável emitir uma Folha e uma Raiz na primeira vez que o usuário solicitar uma licença para uma máquina específica. Se o usuário já tiver a licença Raiz, o servidor poderá emitir apenas uma Folha (chamada de `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar se o cliente já tem uma Raiz aprimorada 3.0). Para solicitações de licença subsequentes, o cliente indicará que já tem uma Folha e uma Raiz, portanto, o servidor deve emitir uma nova licença Raiz. Quando o encadeamento de licenças aprimorado for usado, `setRootKeyRetrievalInfo()` deve ser chamado para fornecer as credenciais necessárias para descriptografar a chave de criptografia raiz na política.

>[!NOTE]
>
>Se a política suportar o Encadeamento de Licenças Aprimorado 3.0, mas o cliente for o Adobe Access 2.0, o servidor emitirá uma licença original 2.0. Para determinar a versão do cliente, use LicenseRequestMessage.getClientVersion().
