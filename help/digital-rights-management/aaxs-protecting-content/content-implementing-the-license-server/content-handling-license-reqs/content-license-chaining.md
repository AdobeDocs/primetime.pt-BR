---
title: Encadeamento de licenças
description: Encadeamento de licenças
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Encadeamento de licenças{#license-chaining}

Se a política usada para gerar a licença der suporte ao encadeamento de licenças, o servidor deverá decidir se emitirá uma licença Leaf, uma licença Root ou ambas. Para determinar o tipo de encadeamento de licenças suportado por uma política, use `Policy.getLicenseChainType()`, ou chame `Policy.getRootLicenseId()` para determinar se a política tem uma licença raiz. Com o encadeamento de licenças do Adobe Access 2.0, o servidor normalmente emite uma licença folha na primeira vez que o usuário solicita uma licença para uma máquina específica e, posteriormente, uma licença raiz. Para determinar se o computador já tem uma licença folha para a política especificada, chame `LicenseRequestMessage.clientHasLeafForPolicy()`.
