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


# Detecção de reversão {#rollback-detection}

Se sua implementação do Adobe Access usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), o Adobe recomenda que o servidor rastreie o contador de reversão e use a listagem de permissão AIR ou SWF.

O contador de reversão é enviado para o servidor na maioria das solicitações do cliente. Se sua implementação do Acesso ao Adobe não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, o Adobe recomenda que o servidor armazene a ID aleatória da máquina, obtida usando `MachineToken.getMachineId().getUniqueId()`, e o valor atual do contador em um banco de dados. Para obter mais informações sobre como aumentar e rastrear o contador de reversão, consulte ClientState em *Referência da API de Acesso ao Adobe* e *Detecção de reversão* em *Usando o SDK de Acesso ao Adobe para Proteção de Conteúdo*.
