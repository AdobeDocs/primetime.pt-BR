---
description: O SDK baixa periodicamente CRLs publicadas pelo Adobe. Você deve garantir que o acesso a esses arquivos não seja bloqueado ou que a aplicação desses CRLs não seja impedida.
title: Consumo de CRLs publicadas pelo Adobe
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Consumo de CRLs publicadas por Adobe{#consuming-crls-published-by-adobe}

O SDK baixa periodicamente CRLs publicadas pelo Adobe. Você deve garantir que o acesso a esses arquivos não seja bloqueado ou que a aplicação desses CRLs não seja impedida.

O SDK tem uma opção de configuração para ignorar erros ao recuperar CRLs de Adobe e você só pode aplicar essa opção em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve recuperar as CRLs do Adobe. Se o servidor de licenças não conseguir obter uma CRL válida, ocorreu um erro.
