---
description: Você pode decidir se deseja resolver somente os anúncios que ocorrem após o ponto ativo atual do usuário ou também resolver os anúncios que ocorrem antes do ponto ativo atual.
title: Carregar anúncio para uma janela DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Carregar anúncio para uma janela DVR {#load-ad-for-a-dvr-window}

Você pode decidir se deseja resolver somente os anúncios que ocorrem após o ponto ativo atual do usuário ou também resolver os anúncios que ocorrem antes do ponto ativo atual.

Quando um usuário começa a visualizar o conteúdo no início de um fluxo de DVR, o TVSDK resolve todos os anúncios do fluxo no momento. No entanto, quando o usuário começa a exibir o conteúdo em um ponto após o início do fluxo, você pode decidir se deseja resolver apenas os anúncios que ocorrem após o ponto ativo atual do usuário ou também resolver os anúncios que ocorreram antes do ponto ativo atual.

>[!TIP]
>
>Resolver anúncios depois do ponto ativo atual é mais rápido, mas se o usuário buscar de trás para frente, essa opção impede que o reprodutor reproduza anúncios que foram exibidos anteriormente.

## Controle e carregamento de uma janela DVR {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Para controlar o carregamento de anúncio de uma janela DVR:

    Para carregar todos os anúncios para todo o fluxo, defina a propriedade &grave;PTAdMetadata.enableDVRAds&#39; como &#39;YES&#39;.

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
