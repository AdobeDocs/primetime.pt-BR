---
title: Integrar seu CDN
description: Integração da CDN
exl-id: b93031a2-6e66-4de1-9cf2-b0260f88fe13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Integrar seu CDN {#integrating-cdn}

O Ad Insertion do Primetime serve como um proxy entre o aplicativo cliente e os manifestos, não as partes do vídeo propriamente ditas. Implante seu conteúdo para o CDN de escolha e transmita o URL para o Primetime Ad Insertion usando a API do Bootstrap. Para obter detalhes sobre a integração, consulte [CDNs compatíveis](/help/primetime-ad-insertion/technical-reference/supported-cdns.md).

## Esquemas de tokenização de CDN compatíveis {#cdn-tokenization-schemes}

As CDNs geralmente têm esquemas de tokenização diferentes para autorização de fragmentos. O Primetime Ad Insertion suporta nativamente as principais redes CDN, incluindo:

* Akamai
* Limelight
* Centurylink / Nível 3
* Entre em contato com o representante de suporte do Primetime para obter uma lista completa de CDNs compatíveis

Para obter mais informações sobre o `pttoken` consulte [Descrição do parâmetro da API do Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md#parameter-description).

## Configurar anúncios a serem entregues a partir do CDN de conteúdo {#configure-ad-deliver-from-cdn}

Talvez você queira fornecer anúncios e conteúdo da mesma CDN para manter a afinidade do conteúdo, ajudar a ignorar os bloqueadores de anúncios e/ou otimizar o número de conexões necessárias do aplicativo cliente. O Primetime Ad Insertion é compatível com regras de regravação de fragmentos para mapear fragmentos ao CDN de conteúdo. Para obter mais informações, consulte [Regravação do manifesto](/help/primetime-ad-insertion/technical-reference/manifest-rewriting.md).

## Aumente o desempenho de inicialização com seu CDN {#increase-startup-performance}

Para obter mais informações, consulte [Otimização da inicialização](/help/primetime-ad-insertion/best-practices/optimize-video-startup-time.md).

## Recursos de várias CDNs {#enable-multi-cdn-fetures}

Entre em contato com o representante do Suporte do Primetime para ativar os recursos de várias CDNs.
