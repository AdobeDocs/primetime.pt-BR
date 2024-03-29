---
title: Visão geral
description: Visão geral
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Visão geral{#overview}

Talvez seja necessário revogar as credenciais de um cliente ou verificar se um determinado conjunto de credenciais já foi revogado sob determinadas condições. As credenciais podem ser revogadas se estiverem comprometidas. Quando esses problemas ocorrem, as licenças não são mais emitidas para clientes comprometidos.

O Adobe mantém Listas de Revogação de Certificados (CRLs) para revogar clientes comprometidos. Essas CRLs são aplicadas automaticamente pelo SDK. Os servidores de licenças podem restringir ainda mais os clientes ao não permitir determinadas credenciais de computador ou versões específicas de DRM e credenciais de tempo de execução. A `RevocationList` pode ser criado e passado para o SDK para revogar credenciais do computador. Determinadas versões de DRM/tempo de execução podem ser revogadas no nível da política de DRM definindo as restrições do módulo no direito de reprodução ou globalmente, definindo as restrições do módulo no `HandlerConfiguration`.

A discussão é centralizada na revogação de credenciais de clientes.
