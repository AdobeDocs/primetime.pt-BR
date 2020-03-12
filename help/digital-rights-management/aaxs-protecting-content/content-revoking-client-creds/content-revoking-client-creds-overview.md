---
seo-title: Revogando credenciais do cliente
title: Revogando credenciais do cliente
uuid: 47f1ec1a-bd8f-4f8c-bee3-bfbf6d9902e7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Revogando credenciais do cliente{#revoking-client-credentials}

Sob determinadas condições, é necessário revogar as credenciais de um cliente ou verificar se um determinado conjunto de credenciais já foi revogado. As credenciais podem ser revogadas se estiverem comprometidas. Quando isso acontecer, as licenças não serão mais emitidas para clientes comprometidos.

A Adobe mantém CRLs (Certificate Revocation Lists, listas de revogação de certificados) para revogar clientes comprometidos. Essas CRLs são automaticamente aplicadas pelo SDK. Os servidores de licença podem restringir ainda mais os clientes ao proibir credenciais de máquina específicas ou versões específicas de DRM e credenciais de tempo de execução. Um arquivo `RevocationList` pode ser criado e passado para o SDK para revogar as credenciais do computador. Versões específicas de DRM/tempo de execução podem ser revogadas no nível da política (ao definir restrições de módulo no direito de reprodução) ou globalmente (ao definir restrições de módulo no `HandlerConfiguration`).

A discussão neste capítulo será centrada na revogação das credenciais do cliente.
