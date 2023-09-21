---
description: A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário aguardar o início da reprodução. O recurso Resolução de carregamento de anúncio lento pode reduzir esse atraso de inicialização. Os anúncios agora podem ser resolvidos em um intervalo especificado antes da posição do ad break. Isso é feito usando uma abordagem de dois jogadores.
title: Resolução de anúncios just-in-time
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Resolução de anúncios just-in-time {#just-in-time-ad-resolving}

A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário aguardar o início da reprodução. O recurso Resolução de carregamento de anúncio lento pode reduzir esse atraso de inicialização. Os anúncios agora podem ser resolvidos em um intervalo especificado antes da posição do ad break. Isso é feito usando uma abordagem de dois jogadores.

**Processo básico de resolução e carregamento de anúncios:**

1. O TVSDK baixa um manifesto (lista de reprodução) e *resolve* todos os anúncios.
1. TVSDK *cargas* todos os anúncios e compila os segmentos de anúncio nos manifestos.
1. O TVSDK move o reprodutor para o status PREPARADO e a reprodução do conteúdo começa.

O reprodutor usa os URLs no manifesto para obter o conteúdo do anúncio (criações), garante que o conteúdo do anúncio esteja em um formato que o TVSDK possa reproduzir e o TVSDK coloca os anúncios na linha do tempo. Esse processo básico de resolução e carregamento de anúncios pode causar um atraso inaceitavelmente longo para um usuário que está aguardando para reproduzir seu conteúdo, especialmente se o manifesto contiver vários URLs de anúncios.

**Resolução de anúncio lento:**

1. O TVSDK baixa a lista de reprodução.
1. TVSDK *resolve e carrega* qualquer anúncio precedente, move o reprodutor para o status PREPARADO e a reprodução do conteúdo é iniciada.
1. TVSDK *resolve* cada ad break antes da posição dele com base no valor definido na `PTAdMetadata::delayAdLoadingTolerance`.

Por exemplo, por padrão `delayAdLoadingTolerance` é definido como 5 segundos. Se um AdBreak for definido para ser reproduzido às 3:00, ele será resolvido às 2:55:00. Você pode aumentar esse valor se acreditar que a resolução do seu anúncio levará mais de 5 segundos.

>[!IMPORTANT]
>
>**Fatores a serem considerados na resolução de anúncios lentos:**
>* A Resolução de Anúncios Lentos só tem suporte para fluxos de VOD com modos de modo de sinalização de anúncios SERVER_MAP.
>* A Resolução de anúncios lenta não é ativada por padrão. Você deve definir `PTAdMetadata::delayAdLoading` = SIM para ativá-lo.
>* A Resolução de Anúncios Lentos é incompatível com o recurso de Ativação Instantânea. Para obter mais informações sobre Ativação instantânea, consulte [Instantâneo](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md).
>* O modo Picture-in-Picture não é compatível com a Resolução Lenta de Anúncios. Desative os modos Picture-in-picture se ativar Resolução de anúncios ociosos.
>* A resolução de anúncios lentos não afeta os anúncios precedentes.
>
**Habilitar resolução de anúncios lentos**

Você pode ativar ou desativar o recurso Resolução de anúncio lento usando o mecanismo de Carregamento de anúncio lento existente (A Resolução de anúncio lento está desativada por padrão).

Você pode ativar a Resolução de anúncios lentos definindo `PTAdMetadata::delayAdLoading`= SIM ao configurar os metadados de anúncios.

**APIs relevantes para resolução de anúncios lentos:**

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
