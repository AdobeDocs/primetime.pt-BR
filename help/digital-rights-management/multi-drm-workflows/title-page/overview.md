---
description: Você pode implementar várias soluções DRM para seus aplicativos TVSDK usando a Nuvem DRM Primetime, com o ExpressPlay. As soluções DRM incluem o FairPlay da Apple, o Widevine do Google, o PlayReady da Microsoft e o Primetime Access da Adobe.
seo-description: Você pode implementar várias soluções DRM para seus aplicativos TVSDK usando a Nuvem DRM Primetime, com o ExpressPlay. As soluções DRM incluem o FairPlay da Apple, o Widevine do Google, o PlayReady da Microsoft e o Primetime Access da Adobe.
seo-title: Visão geral de vários DRM
title: Visão geral de vários DRM
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---


# Workflows Multi-DRM {#multi-drm-workflows}

Você pode implementar várias soluções DRM para seus aplicativos TVSDK usando a Nuvem DRM Primetime, com o ExpressPlay. As soluções DRM incluem o FairPlay da Apple, o Widevine do Google, o PlayReady da Microsoft e o Primetime Access da Adobe.

## Visão geral de vários DRM {#multi-drm-overview}

O Adobe TVSDK oferece suporte à proteção DRM usando vários esquemas DRM. Adobe oferta *Primetime DRM Cloud, com tecnologia ExpressPlay* para fornecer empacotamento, licenciamento e reprodução do conteúdo de vídeo em várias plataformas.

Os esquemas DRM suportados incluem o Primetime Access *DRM (AXS), bem como DRMs nativos em vários dispositivos, incluindo* Widevine[ no Chrome e Android, ](https://www.widevine.com)FairPlay[ no Safari e iOS, e ](https://developer.apple.com/streaming/fps/)PlayReady[ no Edge e no XboxOne. ](https://www.microsoft.com/playready/) Consulte um representante de Adobe para obter informações sobre quais esquemas de DRM estão disponíveis atualmente nessas plataformas, bem como as datas programadas de versões futuras.

O TVSDK oferece suporte a licenças DRM emitidas por qualquer servidor de licenças que use esses protocolos. Além do suporte para várias soluções de DRM, o Adobe oferta *Primetime DRM Cloud, alimentado pelo ExpressPlay* como uma solução na qual o ExpressPlay opera os servidores de licença para cada solução. Isso pode simplificar a configuração e a manutenção para atender às suas necessidades de emissão de licenças de DRM.

Para usar a *Nuvem DRM Primetime, fornecida pelo ExpressPlay* para implementar as suas necessidades de DRM em aplicativos TVSDK, primeiro você deve obter uma conta [ExpressPlay.com](https://www.expressplay.com). O ExpressPlay oferece a capacidade de licenciamento para vários sistemas diferentes de proteção de DRM e também fornece outros serviços, como empacotamento e gerenciamento de chaves.

Seu representante de Adobe irá configurar inicialmente sua conta ExpressPlay. Em seguida, você pode configurar sua conta e obter os *autenticadores do cliente* que você usará em solicitações de token de licença para os servidores ExpressPlay.