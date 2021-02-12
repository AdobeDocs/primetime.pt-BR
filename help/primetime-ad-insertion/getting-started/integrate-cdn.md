---
title: Integrar seu CDN
description: Integração do CDN
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Integrar seu CDN {#integrating-cdn}

O Primetime Ad Insertion serve como proxy entre o aplicativo cliente e os manifestos, e não o vídeo se partes. Implante seu conteúdo para o CDN de sua escolha e passe o URL para o Primetime Ad Insertion usando a API do Bootstrap. Para obter detalhes sobre a integração, consulte [CDNs compatíveis](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## Esquemas de tokenização CDN suportados {#cdn-tokenization-schemes}

As CDNs geralmente têm diferentes esquemas de tokenização para autorização de fragmentos. O Primetime Ad Insertion suporta originalmente as principais redes CDN, incluindo:

* Akamai
* Limitação
* Centurylink / Level3
* Entre em contato com seu representante de suporte Primetime para obter uma lista completa de CDNs suportados

Para obter mais informações sobre o parâmetro `pttoken`, consulte [descrição do parâmetro da API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## Configure os anúncios para entrega a partir do conteúdo CDN {#configure-ad-deliver-from-cdn}

Você pode desejar fornecer anúncios e conteúdo do mesmo CDN para manter a afinidade de conteúdo, ajudar a ignorar bloqueadores de anúncios e/ou otimizar o número de conexões necessárias do aplicativo cliente. O Primetime Ad Insertion suporta regras de regravação de fragmentos para mapear fragmentos para o CDN de conteúdo. Para obter mais informações, consulte [Regravação de manifesto](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## Aumente o desempenho do start com seu CDN {#increase-startup-performance}

Para obter mais informações, consulte [Otimizando start-up](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## Recursos de vários CDN {#enable-multi-cdn-fetures}

Entre em contato com o representante do Suporte Primetime para ativar os recursos de vários CDN.
