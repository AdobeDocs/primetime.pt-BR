---
title: Visão geral do pré-carregamento de licenças para reprodução offline
description: Visão geral do pré-carregamento de licenças para reprodução offline
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Licenças de pré-carregamento para reprodução offline {#pre-loading-licenses-for-offline-playback}

Você pode pré-carregar as licenças necessárias para reproduzir conteúdo protegido pelo Primetime DRM. As licenças pré-carregadas permitem que os usuários visualizem o conteúdo, tenham ou não uma conexão ativa com a Internet.

O próprio processo de pré-carregamento *faz* exigir uma conexão com a Internet. Você pode usar `DRMManager.loadVoucher()` antes do tempo para pré-carregar licenças. Posteriormente, quando o cliente deseja reproduzir o conteúdo desejado, o sistema de DRM foi pré-preparado e pode reproduzir o conteúdo protegido imediatamente.
