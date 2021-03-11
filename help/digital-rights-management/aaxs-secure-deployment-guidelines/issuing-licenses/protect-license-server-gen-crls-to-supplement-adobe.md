---
title: Gerar CRLs para complementar aqueles publicados pelo Adobe
description: Gerar CRLs para complementar aqueles publicados pelo Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Gere CRLs para complementar aqueles publicados pelo Adobe{#generate-crls-to-supplement-those-published-by-adobe}

O Adobe Access permite criar CRLs para complementar a CRL do computador publicada pelo Adobe. O SDK do Adobe Access verifica e aplica as CRLs do Adobe. No entanto, você pode não permitir máquinas cliente adicionais criando uma CRL que revoga credenciais de máquina adicionais. Para fazer isso, você deve passar a CRL para o SDK do Adobe Access e, ao emitir uma licença, o SDK verifica a CRL do Adobe e sua própria CRL.

Para saber mais sobre a geração de CRLs, consulte `RevocationListFactory` em *Referência da API de acesso ao Adobe*.
