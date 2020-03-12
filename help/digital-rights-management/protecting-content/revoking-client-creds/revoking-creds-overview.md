---
seo-title: Visão geral
title: Visão geral
uuid: c6f54867-d0a3-43fd-9493-6496f1b7831a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Visão geral{#overview}

Talvez seja necessário revogar as credenciais de um cliente ou verificar se um determinado conjunto de credenciais já foi revogado em determinadas condições. As credenciais podem ser revogadas se estiverem comprometidas. Quando esses problemas ocorrem, as licenças não são mais emitidas para clientes comprometidos.

A Adobe mantém CRLs (Certificate Revocation Lists, listas de revogação de certificados) para revogar clientes comprometidos. Essas CRLs são automaticamente aplicadas pelo SDK. Os servidores de licença podem restringir ainda mais os clientes ao proibir credenciais de máquina específicas ou versões específicas de DRM e credenciais de tempo de execução. Um arquivo `RevocationList` pode ser criado e passado para o SDK para revogar as credenciais do computador. Versões específicas de DRM/tempo de execução podem ser revogadas no nível de política de DRM, definindo as restrições do módulo à direita ou globalmente, definindo as restrições do módulo no `HandlerConfiguration`.

A discussão está centrada em revogar as credenciais do cliente.
