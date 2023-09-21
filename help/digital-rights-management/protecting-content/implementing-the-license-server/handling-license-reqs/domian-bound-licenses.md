---
title: Emitir licenças vinculadas a domínio
description: Emitir licenças vinculadas a domínio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Emitir licenças vinculadas a domínio{#issuing-domain-bound-licenses}

Para emitir uma licença usando uma política DRM que exija o registro do domínio, a solicitação do cliente deve incluir um token de domínio válido emitido pelo servidor de domínio especificado na política. Quando o cliente solicita uma licença, ele inclui automaticamente seus tokens de domínio para qualquer servidor de domínio especificado nos metadados de conteúdo, desde que tenha se registrado com esses servidores de domínio. Se a política DRM selecionada exigir o registro do domínio, o SDK selecionará automaticamente um token de domínio da solicitação para vincular a licença ou retornará um erro se nenhum token de domínio apropriado for encontrado.

Um token de domínio é considerado válido se não tiver expirado e se tiver sido emitido por uma autoridade de certificação de domínio autorizada. O servidor de licenças deve especificar as autoridades de domínio das quais aceita tokens de domínio configurando `HandlerConfiguration.setDomainCAs()`. Se nenhuma autoridade de certificação de domínio estiver configurada, o servidor de licenças não poderá emitir licenças de domínio associado.

Se os metadados incluírem várias políticas de DRM, a lógica de negócios do servidor de licenças poderá selecionar uma política de DRM baseada no fato de o cliente apresentar ou não um token de domínio. Você pode usar `LicenseRequestMessage.getDomainTokens()` para determinar os domínios com os quais o cliente se registrou.
