---
title: Gerar CRLs para complementar aquelas publicadas pelo Adobe
description: Gerar CRLs para complementar aquelas publicadas pelo Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Gerar CRLs para complementar aquelas publicadas pelo Adobe{#generate-crls-to-supplement-those-published-by-adobe}

O Adobe Access permite que você crie CRLs para complementar a CRL de máquina publicada pelo Adobe. O SDK de acesso do Adobe verifica e impõe as CRLs do Adobe. No entanto, você pode proibir máquinas clientes adicionais criando uma CRL que revogue credenciais de máquina adicionais. Para fazer isso, você deve passar a CRL para o SDK de acesso do Adobe e, ao emitir uma licença, o SDK verificará a CRL do Adobe e sua própria CRL.

Para saber mais sobre a geração de CRLs, consulte `RevocationListFactory` in *Referência da API de acesso do Adobe*.
