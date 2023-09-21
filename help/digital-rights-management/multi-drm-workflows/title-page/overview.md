---
description: Você pode implementar várias soluções DRM para seus aplicativos TVSDK usando o Primetime DRM Cloud, viabilizado pela ExpressPlay. As soluções de DRM incluem o FairPlay da Apple, o Widevine da Google, o PlayReady da Microsoft e o Primetime Access da Adobe.
title: Visão geral de vários DRMs
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Fluxos de trabalho de vários DRM {#multi-drm-workflows}

Você pode implementar várias soluções DRM para seus aplicativos TVSDK usando o Primetime DRM Cloud, viabilizado pela ExpressPlay. As soluções de DRM incluem o FairPlay da Apple, o Widevine da Google, o PlayReady da Microsoft e o Primetime Access da Adobe.

## Visão geral de vários DRMs {#multi-drm-overview}

O Adobe TVSDK oferece suporte à proteção DRM usando vários esquemas DRM. Ofertas Adobe *Primetime DRM Cloud, desenvolvido pela ExpressPlay* para fornecer empacotamento, licenciamento e reprodução de seu conteúdo de vídeo em várias plataformas.

Os esquemas de DRM compatíveis incluem Adobe *Acesso ao Primetime* DRM (AXS), bem como DRMs nativos em vários dispositivos, incluindo [Widevine](https://www.widevine.com) no Chrome e no Android, [FairPlay](https://developer.apple.com/streaming/fps/) no Safari e no iOS, e [PlayReady](https://www.microsoft.com/playready/) no Edge e no XboxOne. Consulte um representante da Adobe para obter informações sobre os esquemas de DRM atualmente disponíveis nessas plataformas, bem como as datas programadas para versões futuras.

O TVSDK é compatível com licenças DRM emitidas por qualquer servidor de licenças que use esses protocolos. Além do suporte para várias soluções de DRM, o Adobe oferece *Primetime DRM Cloud, desenvolvido pela ExpressPlay* como uma solução na qual a ExpressPlay opera os servidores de licença para cada solução. Isso pode simplificar a configuração e a manutenção para as necessidades de emissão de licença de DRM.

Para usar *Primetime DRM Cloud, desenvolvido pela ExpressPlay* para implementar suas necessidades de DRM em aplicativos TVSDK, primeiro obtenha uma [ExpressPlay.com](https://www.expressplay.com) conta. O ExpressPlay oferece o recurso de licenciamento para vários esquemas de proteção DRM diferentes e também fornece outros serviços, incluindo empacotamento e gerenciamento de chaves.

Seu representante da Adobe irá inicialmente configurar sua conta ExpressPlay. Em seguida, você pode configurar sua conta e obter o *autenticadores do cliente* que você usará em solicitações de token de licença para os servidores ExpressPlay.
