---
description: A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário que aguarda o início da reprodução. O recurso de Resolução de Carregamento de Anúncio Preguiçoso pode reduzir esse atraso de inicialização. Os anúncios agora podem ser resolvidos em um intervalo especificado antes da posição do ad break. Isso é feito usando uma abordagem de dois players.
title: Resolver anúncios apenas no tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Resolver anúncios apenas no tempo {#just-in-time-ad-resolving}

A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário que aguarda o início da reprodução. O recurso de Resolução de Carregamento de Anúncio Preguiçoso pode reduzir esse atraso de inicialização. Os anúncios agora podem ser resolvidos em um intervalo especificado antes da posição do ad break. Isso é feito usando uma abordagem de dois players.

**Processo básico de resolução e carregamento de anúncios:**

1. O TVSDK baixa um manifesto (lista de reprodução) e *resolve* todos os anúncios.
1. O TVSDK *carrega* todos os anúncios e une os segmentos de anúncios nos manifestos.
1. O TVSDK move o reprodutor para o status PREPARADO, e a reprodução do conteúdo é iniciada.

O reprodutor usa os URLs no manifesto para obter o conteúdo do anúncio (criações), garante que o conteúdo do anúncio esteja em um formato que TVSDK possa reproduzir e TVSDK coloca os anúncios na linha do tempo. Esse processo básico de resolver e carregar anúncios pode causar um atraso inaceitavelmente longo para um usuário esperando para reproduzir seu conteúdo, especialmente se o manifesto contiver vários URLs de anúncio.

**Resolução de anúncio ocioso:**

1. TVSDK baixa a lista de reprodução.
1. O TVSDK *resolve e carrega* qualquer anúncio precedente, move o reprodutor para o status PREPARADO e a reprodução do conteúdo é iniciada.
1. O TVSDK *resolve* cada ad quebra antes de sua posição com base no valor definido em `PTAdMetadata::delayAdLoadingTolerance`.

Por exemplo, por padrão, `delayAdLoadingTolerance` é definido como 5 segundos. Se um AdBreak estiver definido para ser reproduzido às 3:00, ele será resolvido às 2:55:00. Você pode aumentar esse valor se achar que a resolução da sua publicidade levará mais de 5 segundos.

>[!IMPORTANT]
>
>**Fatores a serem considerados com a resolução de anúncios ociosos:**
>* A resolução de anúncios preguiçosa só é compatível com fluxos VOD somente com modos SERVER_MAP modo de sinalização de anúncios.
>* A resolução de anúncios ociosos não está ativada por padrão. Você deve definir `PTAdMetadata::delayAdLoading` = YES para habilitá-lo.
>* A resolução de anúncios ociosos é incompatível com o recurso Instant On . Para obter mais informações sobre o Instant On, consulte [Instant On](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* O modo Picture-in-Picture não é compatível com a resolução de anúncios preguiçosos. Desative quaisquer modos Picture-in-picture se ativar a Resolução de Anúncios Lento.
>* A resolução de anúncios ociosos não afeta anúncios precedentes.

>


**Habilitar a resolução de anúncio lento**

Você pode ativar ou desativar o recurso de Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçoso (a Resolução de anúncios preguiçosos está desativada por padrão).

Você pode ativar a Resolução de anúncios preguiçosos definindo `PTAdMetadata::delayAdLoading`= SIM ao configurar os metadados de anúncios.

**APIs relevantes para a resolução de anúncios lentos:**

```
Class:    PTAdMetadata 
Properties: 
  
/** 
 * Property to define whether ad break resolution must be delayed until after stream start or not. 
 * When this value is NO, ads are resolved before stream start and spliced into the content when possible allowing  
   for a seamless playback experience. 
 * When this value is YES, ads are displayed in a secondary video player instance and resolved lazily only when  
   needed. 
 * Default value is NO 
 */ 
@property (nonatomic, assign) BOOL delayAdLoading; 
  
/** 
 * Property to define the lookahead for ad break resolution.  Ad breaks will be resolved when they occur between  
   the playhead time and the specified tolerance. 
 * If set to zero, the ad will be resolved immediately before playing the ad.  This may cause a slight delay in the  
   playback of the ads. 
 * Default value is 5.0 or 5 seconds. 
 */ 
  
@property (nonatomic, assign) NSTimeInterval delayAdLoadingTolerance;
```
