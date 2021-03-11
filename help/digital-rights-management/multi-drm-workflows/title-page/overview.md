---
description: É possível implementar várias soluções de DRM para seus aplicativos TVSDK usando a Nuvem de DRM do Primetime, fornecida pela ExpressPlay. As soluções de DRM incluem o FairPlay da Apple, a Widevine do Google, o PlayReady da Microsoft e o Primetime Access do Adobe.
title: Visão geral de vários DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Fluxos de trabalho de vários DRM {#multi-drm-workflows}

É possível implementar várias soluções de DRM para seus aplicativos TVSDK usando a Nuvem de DRM do Primetime, fornecida pela ExpressPlay. As soluções de DRM incluem o FairPlay da Apple, a Widevine do Google, o PlayReady da Microsoft e o Primetime Access do Adobe.

## Visão geral de vários DRM {#multi-drm-overview}

O Adobe TVSDK oferece suporte à proteção de DRM usando vários esquemas de DRM. O Adobe oferece *Primetime DRM Cloud, com a tecnologia ExpressPlay* para fornecer empacotamento, licenciamento e reprodução do conteúdo de vídeo em várias plataformas.

Os esquemas de DRM suportados incluem Adobe *Primetime Access* DRM (AAXS), bem como DRMs nativos em vários dispositivos, incluindo [Widevine](https://www.widevine.com) no Chrome e Android, [FairPlay](https://developer.apple.com/streaming/fps/) no Safari e iOS, e [PlayReady](https://www.microsoft.com/playready/) no Edge e no XboxOne. Consulte um representante de Adobe para obter informações sobre quais esquemas de DRM estão disponíveis atualmente nessas plataformas, bem como as datas programadas de versões futuras.

O TVSDK oferece suporte a licenças DRM emitidas por qualquer servidor de licença que use esses protocolos. Além do suporte para várias soluções de DRM, o Adobe oferece *Primetime DRM Cloud, com ExpressPlay* como uma solução na qual o ExpressPlay opera os servidores de licença para cada solução. Isso pode simplificar a configuração e a manutenção para atender às suas necessidades de emissão de licença de DRM.

Para usar *Primetime DRM Cloud, fornecida pelo ExpressPlay* para implementar suas necessidades de DRM em aplicativos TVSDK, primeiro você deve obter uma conta [ExpressPlay.com](https://www.expressplay.com). O ExpressPlay oferece a capacidade de licenciamento para vários sistemas de proteção de DRM diferentes e também fornece outros serviços, incluindo embalagem e gerenciamento de chaves.

O representante do Adobe configurará inicialmente sua conta ExpressPlay. Em seguida, você pode configurar sua conta e obter os *autenticadores do cliente* que você usará em solicitações de token de licença para os servidores ExpressPlay.