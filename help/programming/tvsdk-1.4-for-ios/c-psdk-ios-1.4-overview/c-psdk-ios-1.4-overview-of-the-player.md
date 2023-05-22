---
description: O TVSDK para iOS inclui vários recursos.
title: Recursos do Primetime TVSDK
exl-id: 1968c072-2651-442d-9e4c-412f7959bcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Recursos do Primetime TVSDK {#primetime-tvsdk-features}

O TVSDK para iOS inclui uma variedade de recursos e fornece os seguintes recursos principais:

* VOD e reprodução ao vivo/linear

   * Gerenciamento da janela de reprodução, incluindo métodos que reproduzem, param, pausam, buscam e recuperam a posição do indicador de reprodução
   * Suporte para repetição completa do evento
   * Closed Caption (608, WebVTT) e formas alternativas de áudio para maior acessibilidade
   * Recurso DVR
   * Lógica da taxa de bits adaptável (ABR) e configuração inicial dos controles ABR
   * Assinatura de tags não HLS e HLS
   * Suporte a failover de manifesto ao vivo

* Publicidade

   * VPAID 2.0
   * Compilação de anúncios do lado do cliente

      * Inserção contínua de anúncios, incluindo suporte para VAST/VMAP
      * Suporte para tags de sinalização personalizadas para anúncios
      * Suporte para marcação, substituição e exclusão de anúncios C3
      * Fluxo de trabalho de inserção de conteúdo/anúncio personalizável, incluindo sinalização de blecaute

* Proteção de conteúdo

   * Acesso a serviços relacionados ao gerenciamento de direitos digitais (DRM)
   * Reprodução de fluxos HLS não criptografados ou com HTTP protegido Live Streaming (PHLS)
   * Controle de saída com base em resolução, com base na política de DRM

* Rastreamento de vídeos e anúncios

   * Rastreamento de evento de QoS
   * Notificações que ajudam o TVSDK e seu aplicativo a se comunicar de forma assíncrona sobre o status de vídeos, anúncios e outros elementos, e também sobre a atividade de log
   * Integração com o Adobe Analytics e suporte ao heartbeat

* Logs

   * Log de depuração
