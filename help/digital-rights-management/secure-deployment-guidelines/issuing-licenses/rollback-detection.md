---
description: Se sua implementação do Adobe Primetime DRM usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), o Adobe recomenda que o servidor acompanhe o contador de reversão e use o AIR ou a lista de permissões do SWF.
title: Detecção de reversão
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Detecção de reversão {#rollback-detection}

Se sua implementação do Adobe Primetime DRM usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), o Adobe recomenda que o servidor acompanhe o contador de reversão e use o AIR ou a lista de permissões do SWF.

O contador de reversão é enviado ao servidor na maioria das solicitações do cliente. Se a implementação do PRIMETIME DRM não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, a Adobe recomenda que o servidor armazene a ID de máquina aleatória, que é obtida usando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())e o valor do contador atual em um banco de dados.

Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e a detecção de reversão.