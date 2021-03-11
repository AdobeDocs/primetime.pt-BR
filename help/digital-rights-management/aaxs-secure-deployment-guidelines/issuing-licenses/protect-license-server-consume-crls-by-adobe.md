---
title: Consume CRLs publicadas pelo Adobe
description: Consume CRLs publicadas pelo Adobe
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# Consume CRLs publicadas por Adobe{#consume-crls-published-by-adobe}

O SDK baixa periodicamente CRLs publicadas pelo Adobe. Não bloqueie o acesso a esses arquivos ou impeça a imposição desses CRLs.

O SDK tem uma opção de configuração para ignorar erros ao recuperar CRLs do Adobe. Essa opção só pode ser usada em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve ser capaz de recuperar as CRLs do Adobe. Falha ao obter uma CRL válida.
