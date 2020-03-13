---
description: Você pode implementar várias soluções DRM para seus aplicativos TVSDK usando a Nuvem DRM Primetime, com o ExpressPlay. As soluções DRM incluem o FairPlay da Apple, o Widevine do Google, o PlayReady da Microsoft e o Primetime Access da Adobe.
seo-description: Você pode implementar várias soluções DRM para seus aplicativos TVSDK usando a Nuvem DRM Primetime, com o ExpressPlay. As soluções DRM incluem o FairPlay da Apple, o Widevine do Google, o PlayReady da Microsoft e o Primetime Access da Adobe.
seo-title: Visão geral de vários DRM
title: Visão geral de vários DRM
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Fluxos de trabalho de vários DRM {#multi-drm-workflows}

Você pode implementar várias soluções DRM para seus aplicativos TVSDK usando a Nuvem DRM Primetime, com o ExpressPlay. As soluções DRM incluem o FairPlay da Apple, o Widevine do Google, o PlayReady da Microsoft e o Primetime Access da Adobe.

## Visão geral de vários DRM {#multi-drm-overview}

O Adobe TVSDK oferece suporte à proteção de DRM usando vários esquemas de DRM. A Adobe oferece a *Primetime DRM Cloud, capacitada pelo ExpressPlay* para fornecer empacotamento, licenciamento e reprodução do conteúdo de vídeo em várias plataformas.

Os esquemas DRM suportados incluem o *Primetime Access* DRM (AAXS) da Adobe, bem como DRMs nativos em vários dispositivos, incluindo o [Widevine](https://www.widevine.com) no Chrome e Android, o [FairPlay](https://developer.apple.com/streaming/fps/) no Safari e iOS e o [PlayReady](https://www.microsoft.com/playready/) no Edge e o XboxOne. Consulte um representante da Adobe para obter informações sobre quais esquemas de DRM estão disponíveis no momento nessas plataformas, bem como as datas programadas de versões futuras.

O TVSDK oferece suporte a licenças DRM emitidas por qualquer servidor de licenças que use esses protocolos. Além de oferecer suporte para várias soluções DRM, a Adobe oferece a *Primetime DRM Cloud, acionada pelo ExpressPlay* como uma solução na qual o ExpressPlay opera os servidores de licença para cada solução. Isso pode simplificar a configuração e a manutenção para atender às suas necessidades de emissão de licenças de DRM.

Para usar a *Primetime DRM Cloud, fornecida pela ExpressPlay* para implementar suas necessidades de DRM em aplicativos TVSDK, primeiro é necessário obter uma conta [ExpressPlay.com](https://www.expressplay.com) . O ExpressPlay oferece a capacidade de licenciamento para vários sistemas diferentes de proteção de DRM e também fornece outros serviços, como empacotamento e gerenciamento de chaves.

Seu representante da Adobe irá configurar sua conta ExpressPlay inicialmente. Em seguida, você pode configurar sua conta e obter os autenticadores *do* cliente que você usará nas solicitações de token de licença para os servidores ExpressPlay.