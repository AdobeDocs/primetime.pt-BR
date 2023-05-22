---
title: Gerar CRLs para complementar aquelas publicadas pelo Adobe
description: Gerar CRLs para complementar aquelas publicadas pelo Adobe
copied-description: true
exl-id: 05dc2159-fa7f-4772-9f25-c89370b4981e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Gerar CRLs para complementar aquelas publicadas pelo Adobe{#generate-crls-to-supplement-those-published-by-adobe}

O Adobe Access permite que você crie CRLs para complementar a CRL de máquina publicada pelo Adobe. O SDK de acesso do Adobe verifica e impõe as CRLs do Adobe. No entanto, você pode proibir máquinas clientes adicionais criando uma CRL que revogue credenciais de máquina adicionais. Para fazer isso, você deve passar a CRL para o SDK de acesso do Adobe e, ao emitir uma licença, o SDK verificará a CRL do Adobe e sua própria CRL.

Para saber mais sobre a geração de CRLs, consulte `RevocationListFactory` in *Referência da API de acesso do Adobe*.
