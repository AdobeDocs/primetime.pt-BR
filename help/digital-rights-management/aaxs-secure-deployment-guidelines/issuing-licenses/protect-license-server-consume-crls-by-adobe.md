---
title: Consumir CRLs publicadas pelo Adobe
description: Consumir CRLs publicadas pelo Adobe
copied-description: true
exl-id: b7f68a29-f834-4613-b64d-e610f660e6fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# Consumir CRLs publicadas pelo Adobe{#consume-crls-published-by-adobe}

O SDK baixa periodicamente as CRLs publicadas pelo Adobe. Não bloquear o acesso a esses arquivos nem impedir a imposição dessas CRLs.

O SDK tem uma opção de configuração para ignorar erros ao recuperar as CRLs de Adobe. Essa opção só pode ser usada em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve ser capaz de recuperar as CRLs do Adobe. A falha ao obter uma CRL válida é um erro.
