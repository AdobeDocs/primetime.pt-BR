---
description: O TVSDK para Android 3.4 inclui uma variedade de recursos que você pode implementar em seus reprodutores.
title: Recursos do Primetime TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# Recursos do Primetime TVSDK {#primetime-tvsdk-features}

O TVSDK para Android 3.9 inclui uma variedade de recursos que você pode implementar em seus reprodutores.

Recursos do TVSDK:

* **VOD e reprodução ao vivo/linear**

   * Gerenciamento da janela de reprodução, incluindo métodos que reproduzem, param, pausam, buscam e recuperam a posição do indicador de reprodução
   * Suporte para repetição completa do evento
   * Closed Caption (608, 708, WebVTT) e formas alternativas de áudio para maior acessibilidade
   * Controles para estilo de texto em legendas
   * Capacidade de DVR, avanço rápido e retrocesso rápido (os dois últimos são conhecidos como *modo de truque*)
   * Lógica da taxa de bits adaptável (ABR) e configuração inicial dos controles ABR
   * Suporte a failover de manifesto ao vivo
   * Buffers de reprodução ajustáveis
   * Suporte ao rastreamento de duração, tamanho e tempo para download do fragmento

* **Publicidade**

   * VPAID 2.0
   * Compilação de anúncios do lado do cliente

      * Inserção contínua de anúncios, incluindo suporte para VAST/VMAP
      * Suporte para tags de sinalização personalizadas para anúncios
      * Suporte para marcação, substituição e exclusão de anúncios C3
      * Fluxo de trabalho de inserção de conteúdo/anúncio personalizável, incluindo sinalização de blecaute

* **Proteção de conteúdo**

   * Acesso a serviços relacionados ao gerenciamento de direitos digitais (DRM)
   * Reprodução de fluxos HLS não criptografados ou com HTTP protegido Live Streaming (PHLS)
   * Controle de saída com base em resolução, com base na política de DRM

* **Rastreamento de vídeos e anúncios**

   * Rastreamento de evento de QoS
   * Notificações que ajudam o TVSDK e seu aplicativo a se comunicar de forma assíncrona sobre o status de vídeos, anúncios e outros elementos. As notificações também registram a atividade.

* **Logs**

   * Log de depuração
   * Suporte de rastreamento para duração, tamanho e tempo de download do fragmento.

* **Entrega segura**

   * Suporte à entrega segura (HTTPS) para todas as chamadas originadas do TVSDK.
