---
title: Emitir licenças vinculadas ao domínio
description: Emitir licenças vinculadas ao domínio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Emitir licenças vinculadas ao domínio{#issuing-domain-bound-licenses}

Para emitir uma licença usando uma política de DRM que exija o registro de domínio, a solicitação do cliente deve incluir um token de domínio válido emitido pelo servidor de domínio especificado na política. Quando o cliente solicita uma licença, ele inclui automaticamente seus tokens de domínio para qualquer servidor de domínio especificado nos metadados de conteúdo fornecidos que tenha registrado com esses servidores de domínio. Se a política de DRM selecionada exigir o registro de domínio, o SDK seleciona automaticamente um token de domínio da solicitação para vincular a licença ou retorna um erro se nenhum token de domínio apropriado tiver sido encontrado.

Um token de domínio é considerado válido se não tiver expirado e se tiver sido emitido por uma autoridade de certificação de domínio autorizada. O servidor de licenças deve especificar as autoridades de domínio das quais aceita tokens de domínio configurando `HandlerConfiguration.setDomainCAs()`. Se nenhuma autoridade de certificação de domínio estiver configurada, o servidor de licenças não poderá emitir licenças vinculadas a domínio.

Se os metadados incluírem várias políticas de DRM, a lógica de negócios do servidor de licenças poderá selecionar uma política de DRM que se baseie no fato de o cliente apresentar um token de domínio. Você pode usar `LicenseRequestMessage.getDomainTokens()` para determinar os domínios com os quais o cliente se registrou.
