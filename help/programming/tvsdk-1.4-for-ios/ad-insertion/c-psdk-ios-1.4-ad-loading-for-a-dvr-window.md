---
description: Você pode decidir se deseja resolver somente os anúncios que ocorrem após o ponto de ativação atual do usuário ou também resolver anúncios que ocorrem antes do ponto de ativação atual.
title: Carregar anúncio para uma janela DVR
exl-id: f0799002-5cba-41c2-86bb-9ccf6b906357
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Carregar anúncio para uma janela DVR {#load-ad-for-a-dvr-window}

Você pode decidir se deseja resolver somente os anúncios que ocorrem após o ponto de ativação atual do usuário ou também resolver anúncios que ocorrem antes do ponto de ativação atual.

Quando um usuário começa a visualizar o conteúdo no início de um fluxo de DVR, o TVSDK resolve todos os anúncios do fluxo nesse momento. No entanto, quando o usuário começa a visualizar o conteúdo em um ponto após o início do fluxo, é possível decidir se deseja resolver somente os anúncios que ocorrem após o ponto de ativação atual do usuário ou também resolver anúncios que ocorreram antes do ponto de ativação atual.

>[!TIP]
>
>Resolver anúncios após o ponto de ativação atual é mais rápido, mas se o usuário buscar de forma retroativa, essa opção impede que o reprodutor reproduza anúncios que apareceram anteriormente.

## Controle e carregamento de uma janela DVR {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Para controlar e carregar uma janela DVR:

Para carregar todos os anúncios para o fluxo inteiro, defina o `PTAdMetadata.enableDVRAds` propriedade para `YES`.

>[!NOTE]
>
>O valor padrão é `NO`, e essa opção carrega anúncios somente do ponto ativo atual.

Por exemplo:

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
 
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
adMetadata.zoneId = <ZoneId>; 
adMetadata.domain = <Domain>; 
 
// Enable DVR Ads by setting to YES the enableDVRAds property on PTAdMetadata  
// (PTAuditudeMetadata is a subclass of PTAdMetadata)  
adMetadata.enableDVRAds = YES; 
 
[metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
 
//Create PTMediaPlayerItem with the previously prepared metadata    
playerItem = [[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata]; 
```
