---
description: O TVSDK para Android 2.5 inclui uma variedade de recursos que você pode implementar em seus players.
seo-description: O TVSDK para Android 2.5 inclui uma variedade de recursos que você pode implementar em seus players.
seo-title: Recursos do Primetime TVSDK
title: Recursos do Primetime TVSDK
uuid: 20ef9abf-1a33-4afc-bb2e-4910e3398a7a
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Recursos do Primetime TVSDK {#primetime-tvsdk-features}

O TVSDK para Android 2.7 inclui uma variedade de recursos que você pode implementar em seus players.

Recursos do TVSDK:

* **Reprodução VOD e ao vivo/linear**

   * Gerenciamento da janela de reprodução, incluindo métodos que reproduzem, param, pausam, buscam e recuperam a posição do indicador de reprodução
   * Suporte para reprodução completa de eventos
   * Legendas ocultas (608, 708, WebVTT) e formas alternativas de áudio para maior acessibilidade
   * Controles para estilo de texto em legendas
   * Recurso DVR, avanço rápido e retrocesso rápido (os dois últimos são conhecidos como modo *de* jogo de truque)
   * Lógica da taxa de bits adaptável (ABR) e configuração inicial dos controles ABR
   * Suporte a failover de manifesto ao vivo
   * Buffers de reprodução ajustáveis
   * Duração, tamanho e tempo de download do fragmento do suporte de rastreamento

* **Publicidade**

   * VPAID 2.0
   * Ajuste de anúncios do cliente

      * Inserção de anúncios simples, incluindo suporte para VAST/VMAP
      * Suporte para tags de sinalização personalizadas para anúncios
      * Suporte para marcação, substituição e exclusão de anúncios C3
      * Fluxo de trabalho personalizável de inserção de conteúdo/anúncio, incluindo sinalização de blecaute

* **Proteção de conteúdo**

   * Acesso a serviços relacionados ao gerenciamento de direitos digitais (DRM)
   * Reprodução de fluxos HLS não criptografados ou com transmissão ao vivo protegida HTTP (PHLS)
   * Controle de saída baseado em resolução, com base na política de DRM

* **Rastreamento de vídeo e anúncio**

   * Rastreamento de eventos QoS
   * Notificações que ajudam o TVSDK e seu aplicativo a se comunicar de forma assíncrona sobre o status de vídeos, anúncios e outros elementos. As notificações também registram a atividade.

* **Registro**

   * Registro de depuração
   * Suporte de rastreamento para duração, tamanho e tempo de download do fragmento.