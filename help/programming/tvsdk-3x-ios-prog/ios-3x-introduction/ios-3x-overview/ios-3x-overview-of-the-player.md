---
description: O TVSDK para Android 3.4 inclui uma variedade de recursos que você pode implementar em seus players.
seo-description: O TVSDK para Android 3.4 inclui uma variedade de recursos que você pode implementar em seus players.
seo-title: Recursos do Primetime TVSDK
title: Recursos do Primetime TVSDK
uuid: 6e26c09c-2858-47d1-80e8-1d7c6a468b86
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Recursos do Primetime TVSDK {#primetime-tvsdk-features}

O TVSDK para iOS inclui uma variedade de recursos que você pode implementar em seus players.

Recursos do TVSDK:

* **Reprodução VOD e ao vivo/linear**

   * Gerenciamento da janela de reprodução, incluindo métodos que reproduzem, param, pausam, buscam e recuperam a posição do indicador de reprodução
   * Suporte para reprodução de evento completo
   * Legendas ocultas (608, 708, WebVTT) e formas alternativas de áudio para aumentar a acessibilidade
   * Controles para estilo de texto em legendas
   * Recurso DVR, avanço rápido e retrocesso rápido (os dois últimos são conhecidos como *modo trick-play*)
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