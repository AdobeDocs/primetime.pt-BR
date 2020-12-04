---
seo-title: Gerar CRLs para complementar os publicados pela Adobe
title: Gerar CRLs para complementar os publicados pela Adobe
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Gerar CRLs para complementar os publicados por Adobe{#generate-crls-to-supplement-those-published-by-adobe}

O Acesso ao Adobe permite que você crie CRLs para complementar a CRL do computador publicada pelo Adobe. O SDK de acesso ao Adobe verifica e impõe as CRLs do Adobe, no entanto, você pode proibir computadores clientes adicionais criando uma CRL que revogue as credenciais adicionais do computador. Para fazer isso, você deve passar a CRL para o SDK de acesso ao Adobe e, ao emitir uma licença, o SDK verifica a CRL do Adobe e sua própria CRL.

Para saber mais sobre a geração de CRLs, consulte `RevocationListFactory` em *Referência da API de Acesso ao Adobe*.
