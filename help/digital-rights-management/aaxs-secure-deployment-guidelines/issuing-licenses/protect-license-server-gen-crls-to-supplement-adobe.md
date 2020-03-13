---
seo-title: Gerar CRLs para complementar os publicados pela Adobe
title: Gerar CRLs para complementar os publicados pela Adobe
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Gerar CRLs para complementar os publicados pela Adobe{#generate-crls-to-supplement-those-published-by-adobe}

O Adobe Access permite que você crie CRLs para complementar a CRL da máquina publicada pela Adobe. O SDK do Adobe Access verifica e impõe as CRLs da Adobe; no entanto, você pode proibir computadores clientes adicionais criando uma CRL que revogue credenciais adicionais do computador. Para fazer isso, você deve passar a CRL para o SDK do Adobe Access e, ao emitir uma licença, o SDK verifica a Adobe CRL e sua própria CRL.

Para saber mais sobre a geração de CRLs, consulte `RevocationListFactory` Adobe Access API Reference **.
