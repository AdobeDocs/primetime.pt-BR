---
title: Detecção de reversão
description: Detecção de reversão
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Detecção de reversão {#rollback-detection}

Se sua implementação do Adobe Access usar regras comerciais que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), o Adobe recomenda que o servidor acompanhe o contador de reversão e use a lista de permissões AIR ou SWF.

O contador de reversão é enviado ao servidor na maioria das solicitações do cliente. Se sua implementação do Acesso ao Adobe não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, o Adobe recomenda que o servidor armazene a ID de máquina aleatória — obtida usando `MachineToken.getMachineId().getUniqueId()` — e o valor do contador atual em um banco de dados. Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte ClientState em *Adobe Access API Reference* e *Rollback detect* em *Using the Adobe Access SDK for Protecting Content*.
