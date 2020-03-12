---
seo-title: Crítica da política de DRM
title: Crítica da política de DRM
uuid: ddc03142-7acb-4a9f-a367-e34cfc5e78ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Crítica da política de DRM{#drm-policy-criticality}

Se você planeja aplicar novas regras de uso em uma política de DRM, e se planeja usar essa política de DRM em conteúdo que foi empacotado para servidores de licença mais antigos (e, portanto, não interpreta corretamente as novas regras de uso), talvez seja necessário especificar como os servidores de licença mais antigos precisam se comportar. Por padrão, a crítica da política do DRM está definida como `true`.

Essa configuração indica que o servidor de licenças deve processar todas as partes da política de DRM antes de poder gerar uma licença que use a política de DRM especificada. Se a crítica da política de DRM estiver definida como `false`, um servidor de licenças mais antigo pode ignorar as partes da política de DRM que não podem ser interpretadas corretamente. Portanto, quaisquer licenças geradas pelo servidor não incluem novas regras de uso.

Os servidores DRM Primetime que suportam a versão 2.0.2 do SDK ou posterior aceitam a configuração de crítica da política DRM.
