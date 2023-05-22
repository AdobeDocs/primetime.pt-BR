---
title: Visão geral do pré-carregamento de licenças para reprodução offline
description: Visão geral do pré-carregamento de licenças para reprodução offline
copied-description: true
exl-id: 0d49c0e4-821b-4354-b92d-bbe2c07e467b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Licenças de pré-carregamento para reprodução offline {#pre-loading-licenses-for-offline-playback}

Você pode pré-carregar as licenças necessárias para reproduzir conteúdo protegido pelo Primetime DRM. As licenças pré-carregadas permitem que os usuários visualizem o conteúdo, tenham ou não uma conexão ativa com a Internet.

O próprio processo de pré-carregamento *faz* exigir uma conexão com a Internet. Você pode usar `DRMManager.loadVoucher()` antes do tempo para pré-carregar licenças. Posteriormente, quando o cliente deseja reproduzir o conteúdo desejado, o sistema de DRM foi pré-preparado e pode reproduzir o conteúdo protegido imediatamente.
