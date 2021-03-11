---
description: O TVSDK para iOS inclui uma variedade de recursos.
title: Recursos do Primetime TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Recursos do Primetime TVSDK {#primetime-tvsdk-features}

O TVSDK para iOS inclui uma variedade de recursos e fornece os principais recursos a seguir:

* Reprodução VOD e ao vivo/linear

   * Gerenciamento da janela de reprodução, incluindo métodos que reproduzem, param, pausam, buscam e recuperam a posição do indicador de reprodução
   * Suporte para repetição completa do evento
   * Legendas ocultas (608, WebVTT) e formas alternativas de áudio para maior acessibilidade
   * Recurso DVR
   * Lógica adaptável de taxa de bits (ABR) e configuração inicial de controles ABR
   * Assinatura de tags não HLS e HLS
   * Suporte a failover de manifesto ao vivo

* Publicidade

   * VPAID 2.0
   * Compilação de anúncios do lado do cliente

      * Inserção de anúncios simples, incluindo suporte para VAST/VMAP
      * Suporte para tags de sinalização personalizadas para anúncios
      * Suporte para marcação, substituição e exclusão de anúncios C3
      * Fluxo de trabalho personalizável de inserção de conteúdo/anúncio, incluindo sinalização de blecaute

* Proteção de conteúdo

   * Acesso a serviços relacionados ao gerenciamento de direitos digitais (DRM)
   * Reprodução de fluxos HLS não criptografados ou com HTTP Live Streaming (PHLS) protegido
   * Controle de saída baseado em resolução, com base na política de DRM

* Rastreamento de vídeo e anúncio

   * Rastreamento de eventos de QoS
   * Notificações que ajudam o TVSDK e seu aplicativo a se comunicar de forma assíncrona sobre o status de vídeos, anúncios e outros elementos, e também sobre a atividade de log
   * Integração com o Adobe Analytics e suporte a pulsações

* Registro

   * Registro de depuração

