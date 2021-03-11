---
title: Revogando credenciais de cliente
description: Revogando credenciais de cliente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Revogando credenciais de cliente{#revoking-client-credentials}

Sob determinadas condições, é necessário revogar as credenciais de um cliente ou verificar se um determinado conjunto de credenciais já foi revogado. As credenciais podem ser revogadas se as credenciais forem comprometidas. Quando isso acontecer, as licenças não serão mais emitidas para clientes comprometidos.

O Adobe mantém CRLs (Certificate Revocation Lists, listas de revogação de certificados) para revogar clientes comprometidos. Essas CRLs são aplicadas automaticamente pelo SDK. Os servidores de licença podem restringir ainda mais os clientes ao não permitir credenciais de máquina específicas ou versões específicas de DRM e credenciais de tempo de execução. Um `RevocationList` pode ser criado e passado para o SDK a fim de revogar credenciais de máquina. Versões específicas de DRM/tempo de execução podem ser revogadas no nível da política (definindo restrições de módulo no direito de reprodução) ou globalmente (definindo restrições de módulo no `HandlerConfiguration`).

A discussão neste capítulo será centrada na revogação das credenciais do cliente.
