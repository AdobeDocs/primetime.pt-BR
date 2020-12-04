---
seo-title: Consumir CRLs publicadas pela Adobe
title: Consumir CRLs publicadas pela Adobe
uuid: 43f65edb-0c96-46ab-b787-1b5f0b4b093e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Consumir CRLs publicadas por Adobe{#consume-crls-published-by-adobe}

O SDK baixa periodicamente CRLs publicadas pelo Adobe. Não bloqueie o acesso a esses arquivos nem impeça a aplicação dessas CRLs.

O SDK tem uma opção de configuração para ignorar erros ao recuperar CRLs de Adobe. Essa opção só pode ser usada em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve ser capaz de recuperar as CRLs do Adobe. Falha ao obter uma CRL válida é um erro.
