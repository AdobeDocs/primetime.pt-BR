---
title: Encadeamento de licenças aprimorado
description: Encadeamento de licenças aprimorado
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Encadeamento de licenças aprimorado {#enhanced-license-chaining}

Com o aprimoramento do encadeamento de licenças no Adobe Access 3.0, é recomendável emitir uma Folha e uma Raiz na primeira vez que o usuário solicitar uma licença para uma máquina específica. Se o usuário já tiver a licença Raiz, o servidor poderá emitir apenas uma Folha (chamada de `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` para determinar se o cliente já tem uma Raiz aprimorada 3.0). Para solicitações de licença subsequentes, o cliente indicará que já tem uma Folha e uma Raiz, portanto, o servidor deve emitir uma nova licença Raiz. Quando o encadeamento de licenças aprimorado é usado, `setRootKeyRetrievalInfo()` deve ser chamado para fornecer as credenciais necessárias para descriptografar a chave de criptografia raiz na política.

>[!NOTE]
>
>Se a política suportar o Encadeamento de Licenças Aprimorado 3.0, mas o cliente for o Adobe Access 2.0, o servidor emitirá uma licença original 2.0. Para determinar a versão do cliente, use LicenseRequestMessage.getClientVersion().
