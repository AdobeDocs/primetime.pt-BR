---
seo-title: Pré-carregar licenças para reprodução offline visão geral
title: Pré-carregar licenças para reprodução offline visão geral
uuid: 71e5169b-7f70-4723-9f9b-fdff822c5876
translation-type: tm+mt
source-git-commit: 9bbcb228d3367fbf53de811bf2941ca653ce3b0e

---


# Pré-carregar licenças para reprodução offline {#pre-loading-licenses-for-offline-playback}

Você pode pré-carregar as licenças necessárias para reproduzir conteúdo protegido pelo Primetime DRM. As licenças pré-carregadas permitem que os usuários visualizem o conteúdo, independentemente de terem ou não uma conexão ativa com a Internet.

O próprio processo de pré-carregamento *requer* uma conexão com a Internet. Você pode usar com antecedência `DRMManager.loadVoucher()` para pré-carregar licenças. Posteriormente, quando o cliente deseja reproduzir o conteúdo desejado, o sistema DRM foi pré-inicializado e pode reproduzir o conteúdo protegido imediatamente.
