---
title: Detecção de reversão
description: Detecção de reversão
copied-description: true
exl-id: 054d3634-5ce9-4a51-ac91-e6ae60a1fd6e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# Detecção de reversão {#rollback-detection}

Se sua implementação do Acesso ao Adobe usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), o Adobe recomenda que o servidor acompanhe o contador de reversão e use o AIR ou a lista de permissões do SWF.

O contador de reversão é enviado ao servidor na maioria das solicitações do cliente. Se sua implementação do Acesso ao Adobe não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, a Adobe recomenda que o servidor armazene a ID de máquina aleatória - obtida usando `MachineToken.getMachineId().getUniqueId()`—e o valor do contador atual em um banco de dados. Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte ClientState em *Referência da API de acesso do Adobe* e *Detecção de reversão* in *Utilização do SDK do Adobe Access para proteção de conteúdo*.
