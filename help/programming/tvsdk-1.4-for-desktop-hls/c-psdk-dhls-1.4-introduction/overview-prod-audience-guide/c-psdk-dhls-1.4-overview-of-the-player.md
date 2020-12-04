---
description: 'O TVSDK para HLS de desktop inclui uma variedade de recursos e fornece os seguintes recursos principais '
seo-description: 'O TVSDK para HLS de desktop inclui uma variedade de recursos e fornece os seguintes recursos principais '
seo-title: Recursos do Primetime TVSDK
title: Recursos do Primetime TVSDK
uuid: 0a7ebb05-7da5-49ff-928a-4d2124eaa115
translation-type: tm+mt
source-git-commit: 25a0dfef12ecf10ba939500c4ba539468c41ee1b
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Recursos do Primetime TVSDK{#primetime-tvsdk-features}

O TVSDK for Desktop HLS inclui uma variedade de recursos e fornece os seguintes recursos principais:

* Reprodução VOD e ao vivo/linear

   * Gerenciamento da janela de reprodução, incluindo métodos que reproduzem, param, pausam, buscam e recuperam a posição do indicador de reprodução.
   * Legendas ocultas (608, 708, WebVTT) e formas alternativas de áudio para aumentar a acessibilidade
   * Controle para estilização de texto em legendas
   * Recurso DVR, retrocesso rápido para frente/rápido (modo de jogo de truques)
   * Reprodução de truques para conteúdo ao vivo e VOD
   * Lógica da taxa de bits adaptável (ABR) e configuração inicial dos controles ABR
   * Suporte a failover de manifesto ao vivo
   * Buffers de reprodução ajustáveis
   * Otimização de redirecionamento 302
   * Duração, tamanho e tempo de download do fragmento do suporte de rastreamento

* Publicidade

   * VPAID 2.0
   * Ajuste de anúncios do cliente

      * Inserção de anúncios simples, incluindo suporte para VAST/VMAP
      * Suporte para tags de sinalização personalizadas para anúncios
      * Suporte para marcação, substituição e exclusão de anúncios C3
      * Fluxo de trabalho personalizável de inserção de conteúdo/anúncio, incluindo sinalização de blecaute

* Proteção de conteúdo

   * Acesso a serviços relacionados ao gerenciamento de direitos digitais (DRM)
   * Reprodução de fluxos HLS não criptografados ou com transmissão ao vivo protegida HTTP (PHLS)
   * Controle de saída baseado em resolução, com base na política de DRM
   * Suporte a cookies de sessão e cookies de autenticação de mídia
   * Pacote de token de vários domínios

* Rastreamento de vídeo e anúncio

   * Rastreamento de eventos QoS
   * Notificações que ajudam o TVSDK e seu aplicativo a se comunicar de forma assíncrona sobre o status de vídeos, anúncios e outros elementos, além da atividade de log.
   * Integração com o Adobe Analytics e suporte a pulsação

* Registro

   * Registro de depuração.
   * Suporte de rastreamento para duração, tamanho e tempo de download do fragmento.