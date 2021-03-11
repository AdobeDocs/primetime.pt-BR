---
title: Cadeamento de licença
description: Cadeamento de licença
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Cadeamento de licença{#license-chaining}

Se a política usada para gerar a licença suportar encadeamento de licenças, o servidor deverá decidir se deseja emitir uma licença Folha, uma licença Raiz ou ambos. Para determinar o tipo de licença que uma política suporta, use `Policy.getLicenseChainType()` ou chame `Policy.getRootLicenseId()` para determinar se a política tem uma licença raiz. Com o encadeamento da licença do Adobe Access 2.0, o servidor normalmente emite uma licença de folha na primeira vez que o usuário solicita uma licença para uma máquina específica e uma licença de raiz posteriormente. Para determinar se a máquina já tem uma licença de folha para a política especificada, chame `LicenseRequestMessage.clientHasLeafForPolicy()`.
