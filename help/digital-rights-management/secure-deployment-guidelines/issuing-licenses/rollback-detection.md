---
description: Se sua implementação do Adobe Primetime DRM usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), a Adobe recomenda que o servidor rastreie o contador de reversão e use a lista de permissões AIR ou SWF.
seo-description: Se sua implementação do Adobe Primetime DRM usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), a Adobe recomenda que o servidor rastreie o contador de reversão e use a lista de permissões AIR ou SWF.
seo-title: Detecção de retorno
title: Detecção de retorno
uuid: f161ed41-488a-478a-b6a8-468cf6d11e89
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c

---


# Detecção de retorno {#rollback-detection}

Se sua implementação do Adobe Primetime DRM usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), a Adobe recomenda que o servidor rastreie o contador de reversão e use a lista de permissões AIR ou SWF.

O contador de reversão é enviado para o servidor na maioria das solicitações do cliente. Se a implementação do Primetime DRM não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, a Adobe recomenda que o servidor armazene a ID aleatória da máquina, que é obtida usando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), e o valor atual do contador em um banco de dados.

Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte Detecção de [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e Reversão.