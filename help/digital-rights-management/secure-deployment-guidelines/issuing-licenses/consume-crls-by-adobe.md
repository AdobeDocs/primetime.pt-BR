---
description: O SDK baixa periodicamente as CRLs publicadas pelo Adobe. Você deve garantir que o acesso a esses arquivos não seja bloqueado ou que a imposição dessas CRLs não seja impedida.
title: Consumindo CRLs publicadas pelo Adobe
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Consumindo CRLs publicadas pelo Adobe{#consuming-crls-published-by-adobe}

O SDK baixa periodicamente as CRLs publicadas pelo Adobe. Você deve garantir que o acesso a esses arquivos não seja bloqueado ou que a imposição dessas CRLs não seja impedida.

O SDK tem uma opção de configuração para ignorar erros ao recuperar CRLs de Adobe, e você só pode aplicar essa opção em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve recuperar as CRLs do Adobe. Ocorreu um erro se o servidor de licenças não puder obter uma CRL válida.
