---
title: Integrar seu CDN
description: Integração do CDN
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Integrar seu CDN {#integrating-cdn}

O Primetime Ad Insertion serve como proxy entre o aplicativo cliente e os manifestos, e não o vídeo se partes. Implante seu conteúdo para o CDN de sua escolha e passe o URL para o Primetime Ad Insertion usando a API do Bootstrap.<!-- For integration details, see [Supported CDNs](supported-cdns.md).-->

## Esquemas de tokenização CDN suportados {#cdn-tokenization-schemes}

As CDNs geralmente têm diferentes esquemas de tokenização para autorização de fragmentos. O Primetime Ad Insertion suporta originalmente as principais redes CDN, incluindo:

* Akamai
* Limitação
* Centurylink / Level3
* Entre em contato com seu representante de suporte Primetime para obter uma lista completa de CDNs suportados

Para obter mais informações sobre o parâmetro `pttoken`, consulte [descrição do parâmetro da API do Bootstrap](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md).

## Configure os anúncios para entrega a partir do conteúdo CDN {#configure-ad-deliver-from-cdn}

Você pode desejar fornecer anúncios e conteúdo do mesmo CDN para manter a afinidade de conteúdo, ajudar a ignorar bloqueadores de anúncios e/ou otimizar o número de conexões necessárias do aplicativo cliente. O Primetime Ad Insertion suporta regras de regravação de fragmentos para mapear fragmentos para o CDN de conteúdo.

<!--## Increase start-up performance with your CDN {#increase-startup-performance}

For more information, see [Optimizing start-up](optimize-video-startup-time.md).-->

## Recursos de vários CDN {#enable-multi-cdn-fetures}

Entre em contato com o representante do Suporte Primetime para ativar os recursos de vários CDN.
