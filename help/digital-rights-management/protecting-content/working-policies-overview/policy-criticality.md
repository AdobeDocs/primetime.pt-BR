---
title: Importalidade da política de DRM
description: Importalidade da política de DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Importalidade da política de DRM{#drm-policy-criticality}

Se você planeja aplicar novas regras de uso em uma política DRM e planeja usar essa política DRM no conteúdo que foi empacotado para servidores de licença mais antigos (e, portanto, não interpreta corretamente as novas regras de uso), talvez seja necessário especificar como os servidores de licença mais antigos precisam se comportar. Por padrão, a criticidade da política de DRM é definida como `true`.

Esta configuração indica que o servidor de licença deve processar todas as partes da política DRM antes de gerar uma licença que use a política DRM especificada. Se a criticalidade da política de DRM estiver definida como `false`, um servidor de licença mais antigo pode ignorar as partes da política de DRM que não podem ser interpretadas corretamente. Portanto, as licenças geradas pelo servidor não incluem novas regras de uso.

Os servidores DRM do Primetime com suporte à versão 2.0.2 ou posterior do SDK aceitam a configuração de criticidade de política de DRM.
