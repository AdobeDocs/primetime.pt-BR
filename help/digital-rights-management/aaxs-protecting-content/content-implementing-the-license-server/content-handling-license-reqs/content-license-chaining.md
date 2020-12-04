---
seo-title: Cadeamento de licença
title: Cadeamento de licença
uuid: dcc12663-ef9e-4c73-b837-66fcec39358b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Cadeamento de licença{#license-chaining}

Se a política usada para gerar a licença suportar encadeamento de licença, o servidor deverá decidir se deseja emitir uma licença Folha, uma licença Raiz ou ambos. Para determinar que tipo de licença um encadeamento de política suporta, use `Policy.getLicenseChainType()` ou chame `Policy.getRootLicenseId()` para determinar se a política tem uma licença raiz. Com o encadeamento de licença do Adobe Access 2.0, o servidor geralmente emite uma licença de folha na primeira vez que o usuário solicita uma licença para uma máquina específica e uma licença de raiz posteriormente. Para determinar se o computador já tem uma licença de folha para a política especificada, chame `LicenseRequestMessage.clientHasLeafForPolicy()`.
