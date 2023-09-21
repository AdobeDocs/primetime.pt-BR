---
title: Consumir CRLs publicadas pelo Adobe
description: Consumir CRLs publicadas pelo Adobe
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Consumir CRLs publicadas pelo Adobe{#consume-crls-published-by-adobe}

O SDK baixa periodicamente as CRLs publicadas pelo Adobe. Não bloquear o acesso a esses arquivos nem impedir a imposição dessas CRLs.

O SDK tem uma opção de configuração para ignorar erros ao recuperar as CRLs de Adobe. Essa opção só pode ser usada em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve ser capaz de recuperar as CRLs do Adobe. A falha ao obter uma CRL válida é um erro.
