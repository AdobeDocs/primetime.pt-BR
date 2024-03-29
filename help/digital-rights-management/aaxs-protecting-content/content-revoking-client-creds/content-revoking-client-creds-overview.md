---
title: Revogação de credenciais do cliente
description: Revogação de credenciais do cliente
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Revogação de credenciais do cliente{#revoking-client-credentials}

Em determinadas condições, é necessário revogar as credenciais de um cliente ou verificar se um determinado conjunto de credenciais já foi revogado. As credenciais podem ser revogadas se estiverem comprometidas. Quando isso acontecer, as licenças não serão mais emitidas para clientes comprometidos.

O Adobe mantém Listas de Revogação de Certificados (CRLs) para revogar clientes comprometidos. Essas CRLs são aplicadas automaticamente pelo SDK. Os servidores de licenças podem restringir ainda mais os clientes ao não permitir determinadas credenciais de computador ou versões específicas de DRM e credenciais de tempo de execução. A `RevocationList` pode ser criado e passado para o SDK para revogar credenciais do computador. Determinadas versões de DRM/tempo de execução podem ser revogadas no nível da política (definindo restrições do módulo no direito de reprodução) ou globalmente (definindo restrições do módulo no `HandlerConfiguration`).

A discussão deste capítulo será centralizada na revogação de credenciais de clientes.
