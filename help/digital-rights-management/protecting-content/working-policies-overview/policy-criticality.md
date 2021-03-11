---
title: Crítica da política de DRM
description: Crítica da política de DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Crítica da política de DRM{#drm-policy-criticality}

Se você planeja aplicar novas regras de uso em uma política de DRM e se planeja usar essa política de DRM no conteúdo que foi empacotado para servidores de licença mais antigos (e, portanto, não interpreta corretamente as novas regras de uso), talvez seja necessário especificar como os servidores de licença mais antigos precisam se comportar. Por padrão, a crítica da política de DRM é definida como `true`.

Esta configuração indica que o servidor de licenças deve processar todas as partes da política de DRM antes de poder gerar uma licença que use a política de DRM especificada. Se a crítica da política de DRM estiver definida como `false`, um servidor de licenças mais antigo poderá ignorar as partes da política de DRM que não pode interpretar corretamente. Portanto, as licenças geradas pelo servidor não incluem novas regras de uso.

Os servidores DRM Primetime que oferecem suporte à versão 2.0.2 do SDK ou posterior aceitam a configuração de criticalidade da política DRM.
