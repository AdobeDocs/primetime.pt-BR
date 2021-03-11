---
title: Visão geral
description: Visão geral
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Visão geral{#overview}

Talvez seja necessário revogar as credenciais de um cliente ou verificar se um determinado conjunto de credenciais já foi revogado em determinadas condições. As credenciais podem ser revogadas se estiverem comprometidas. Quando esses problemas ocorrem, as licenças não são mais emitidas para clientes comprometidos.

O Adobe mantém CRLs (Certificate Revocation Lists, listas de revogação de certificados) para revogar clientes comprometidos. Essas CRLs são aplicadas automaticamente pelo SDK. Os servidores de licença podem restringir ainda mais os clientes ao não permitir credenciais de máquina específicas ou versões específicas de DRM e credenciais de tempo de execução. Um `RevocationList` pode ser criado e passado para o SDK a fim de revogar credenciais de máquina. Determinadas versões de DRM/tempo de execução podem ser revogadas no nível da política de DRM, definindo restrições de módulo no direito de reprodução ou globalmente, definindo restrições de módulo no `HandlerConfiguration`.

A discussão está centrada na revogação das credenciais do cliente.
