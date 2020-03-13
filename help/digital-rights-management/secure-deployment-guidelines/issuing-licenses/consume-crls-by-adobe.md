---
description: O SDK baixa periodicamente CRLs publicadas pela Adobe. Você deve garantir que o acesso a esses arquivos não esteja bloqueado ou que a aplicação dessas CRLs não seja impedida.
seo-description: O SDK baixa periodicamente CRLs publicadas pela Adobe. Você deve garantir que o acesso a esses arquivos não esteja bloqueado ou que a aplicação dessas CRLs não seja impedida.
seo-title: Consumir CRLs publicadas pela Adobe
title: Consumir CRLs publicadas pela Adobe
uuid: 7a9088bd-dde6-4445-958c-3e7272215b3c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Consumir CRLs publicadas pela Adobe{#consuming-crls-published-by-adobe}

O SDK baixa periodicamente CRLs publicadas pela Adobe. Você deve garantir que o acesso a esses arquivos não esteja bloqueado ou que a aplicação dessas CRLs não seja impedida.

O SDK tem uma opção de configuração para ignorar erros ao recuperar CRLs da Adobe, e você só pode aplicar essa opção em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve recuperar as CRLs da Adobe. Se o servidor de licenças não conseguir obter uma CRL válida, ocorreu um erro.
