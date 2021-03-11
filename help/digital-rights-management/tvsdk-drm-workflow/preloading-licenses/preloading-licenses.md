---
title: Visão geral das licenças de pré-carregamento para reprodução offline
description: Visão geral das licenças de pré-carregamento para reprodução offline
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# Licenças de pré-carregamento para reprodução offline {#pre-loading-licenses-for-offline-playback}

Você pode pré-carregar as licenças necessárias para reproduzir conteúdo protegido pelo DRM do Primetime. As licenças pré-carregadas permitem que os usuários visualizem o conteúdo, independentemente de terem ou não uma conexão ativa com a Internet.

O próprio processo de pré-carregamento *faz* necessita de uma ligação à Internet. Você pode usar `DRMManager.loadVoucher()` antecipadamente para pré-carregar as licenças. Posteriormente, quando o cliente deseja reproduzir o conteúdo desejado, o sistema DRM foi pré-preparado e pode reproduzir o conteúdo protegido imediatamente.
