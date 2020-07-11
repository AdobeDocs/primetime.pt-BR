---
seo-title: Detecção de retorno
title: Detecção de retorno
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Detecção de retorno {#rollback-detection}

Se sua implementação do Adobe Access usar regras de negócios que exijam que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), a Adobe recomenda que o servidor rastreie o contador de reversão e use a lista de permissão AIR ou SWF.

O contador de reversão é enviado para o servidor na maioria das solicitações do cliente. Se sua implementação do Adobe Access não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, a Adobe recomenda que o servidor armazene a ID aleatória da máquina, obtida usando `MachineToken.getMachineId().getUniqueId()`— e o valor atual do contador em um banco de dados. Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte ClientState em *Adobe Access API Reference* e detecção *de* reversão em *Using the Adobe Access SDK for Protecting Content*.
