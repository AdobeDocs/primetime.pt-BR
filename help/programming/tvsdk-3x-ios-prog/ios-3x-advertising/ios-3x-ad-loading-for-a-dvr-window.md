---
description: Você pode decidir se deseja resolver somente os anúncios que ocorrem após o ponto ativo atual do usuário ou também resolver os anúncios que ocorrem antes do ponto ativo atual.
seo-description: Você pode decidir se deseja resolver somente os anúncios que ocorrem após o ponto ativo atual do usuário ou também resolver os anúncios que ocorrem antes do ponto ativo atual.
seo-title: Carregar anúncio para uma janela DVR
title: Carregar anúncio para uma janela DVR
uuid: 3ae1fbf6-deae-4f39-a17d-43d1fe3cb975
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Carregar anúncio para uma janela DVR {#load-ad-for-a-dvr-window}

Você pode decidir se deseja resolver somente os anúncios que ocorrem após o ponto ativo atual do usuário ou também resolver os anúncios que ocorrem antes do ponto ativo atual.

Quando um usuário começa a exibir o conteúdo no início de um fluxo DVR, o TVSDK resolve todos os anúncios do fluxo naquele momento. No entanto, quando o usuário começa a exibir o conteúdo em um ponto após o início do fluxo, você pode decidir se deseja resolver apenas os anúncios que ocorrem após o ponto ativo atual do usuário ou também resolver os anúncios que ocorreram antes do ponto ativo atual.

>[!TIP]
>
>A resolução de anúncios após o ponto ativo atual é mais rápida, mas se o usuário buscar para trás, essa opção impede que o player reproduza anúncios que apareceram antes.

## Controlar o carregamento de um anúncio para uma janela DVR {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Para controlar o carregamento de um anúncio para uma janela DVR:

    Para carregar todos os anúncios para o fluxo inteiro, defina a propriedade &quot;PTAdMetadata.enableDVRAds&quot; como &quot;YES&quot;.

>[!NOTE]
>
>O valor padrão é `NO`, e essa opção carrega publicidades somente do ponto ativo atual.

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
