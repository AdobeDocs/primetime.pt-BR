---
title: Detecção de reversão
description: Detecção de reversão
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Detecção de reversão {#rollback-detection}

Se sua implementação do Acesso ao Adobe usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), o Adobe recomenda que o servidor acompanhe o contador de reversão e use o AIR ou a lista de permissões do SWF.

O contador de reversão é enviado ao servidor na maioria das solicitações do cliente. Se sua implementação do Acesso ao Adobe não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, a Adobe recomenda que o servidor armazene a ID de máquina aleatória - obtida usando `MachineToken.getMachineId().getUniqueId()`—e o valor do contador atual em um banco de dados. Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte ClientState em *Referência da API de acesso do Adobe* e *Detecção de reversão* in *Utilização do SDK do Adobe Access para proteção de conteúdo*.
