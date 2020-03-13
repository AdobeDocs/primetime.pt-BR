---
seo-title: Emitindo licenças de domínio
title: Emitindo licenças de domínio
uuid: 706650b7-6044-4c01-9f5a-90779127c9e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Emitindo licenças de domínio{#issuing-domain-bound-licenses}

Para emitir uma licença usando uma política de DRM que exija registro de domínio, a solicitação do cliente deve incluir um token de domínio válido emitido pelo servidor de domínio especificado na política. Quando o cliente solicita uma licença, ele inclui automaticamente seus tokens de domínio para qualquer servidor de domínio especificado nos metadados de conteúdo fornecidos que se registrou nesses servidores de domínio. Se a política DRM selecionada exigir o registro do domínio, o SDK seleciona automaticamente um token de domínio da solicitação para vincular a licença ou retorna um erro se nenhum token de domínio apropriado tiver sido encontrado.

Um token de domínio é considerado válido se não tiver expirado e se tiver sido emitido por uma AC de domínio autorizada. O servidor de licenças deve especificar as autoridades de domínio a partir das quais aceita tokens de domínio configurando `HandlerConfiguration.setDomainCAs()`. Se nenhuma CAs de domínio estiver configurada, o servidor de licenças não poderá emitir licenças de domínio.

Se os metadados incluírem várias políticas de DRM, a lógica comercial do servidor de licenças poderá selecionar uma política de DRM baseada no fato de o cliente apresentar um token de domínio. Você pode usar `LicenseRequestMessage.getDomainTokens()` para determinar os domínios com os quais o cliente se registrou.
