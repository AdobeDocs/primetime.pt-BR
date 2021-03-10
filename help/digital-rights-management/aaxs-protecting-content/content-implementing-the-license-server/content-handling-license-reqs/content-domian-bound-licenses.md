---
title: Emitir licenças de domínio
description: Emitir licenças de domínio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Emitir licenças vinculadas ao domínio{#issuing-domain-bound-licenses}

Para emitir uma licença usando uma política que exija o registro de domínio, a solicitação do cliente deve incluir um token de domínio válido emitido pelo servidor de domínio especificado na política. Quando o cliente solicita uma licença, ele incluirá automaticamente seus tokens de domínio para qualquer servidor de domínio especificado nos metadados de conteúdo, se tiver se registrado nesses servidores de domínio. Se a política selecionada exigir o registro de domínio, o SDK selecionará automaticamente um token de domínio da solicitação para vincular a licença ou retornará um erro se nenhum token de domínio apropriado tiver sido encontrado.

Um token de domínio é considerado válido se não tiver expirado e se tiver sido emitido por uma autoridade de certificação de domínio autorizada. O servidor de licenças deve especificar as autoridades de domínio das quais aceitará tokens de domínio configurando `HandlerConfiguration.setDomainCAs()`. Se nenhuma autoridade de certificação de domínio estiver configurada, o servidor de licenças não poderá emitir licenças vinculadas a domínio.

Se os metadados incluírem várias políticas, a lógica comercial do servidor de licenças poderá selecionar uma política com base em se o cliente apresentou um token de domínio. Use `LicenseRequestMessage.getDomainTokens()` para determinar os domínios com os quais o cliente se registrou.
