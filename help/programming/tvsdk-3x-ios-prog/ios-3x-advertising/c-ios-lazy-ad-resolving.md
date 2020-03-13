---
description: A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera o início da reprodução. O recurso Resolução de carregamento lento de anúncio pode reduzir esse atraso de inicialização. Os anúncios agora podem ser resolvidos em um intervalo especificado antes da posição do intervalo do anúncio. Isso é feito usando uma abordagem de dois jogadores.
seo-description: A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera o início da reprodução. O recurso Resolução de carregamento lento de anúncio pode reduzir esse atraso de inicialização. Os anúncios agora podem ser resolvidos em um intervalo especificado antes da posição do intervalo do anúncio. Isso é feito usando uma abordagem de dois jogadores.
seo-title: Solução de anúncios just-in-time
title: Solução de anúncios just-in-time
uuid: f7b20439-3604-4d69-bdfe-2e0ad26f495b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Solução de anúncios just-in-time {#just-in-time-ad-resolving}

A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera o início da reprodução. O recurso Resolução de carregamento lento de anúncio pode reduzir esse atraso de inicialização. Os anúncios agora podem ser resolvidos em um intervalo especificado antes da posição do intervalo do anúncio. Isso é feito usando uma abordagem de dois jogadores.

**Processo básico de resolução e carregamento de anúncios:**

1. O TVSDK baixa um manifesto (lista de reprodução) e *resolve* todos os anúncios.
1. O TVSDK *carrega* todos os anúncios e une os segmentos de anúncios nos manifestos.
1. O TVSDK move o player para o status PREPARADO e a reprodução do conteúdo é iniciada.

O player usa os URLs no manifesto para obter o conteúdo do anúncio (criativos), garante que o conteúdo do anúncio esteja em um formato que o TVSDK possa reproduzir e o TVSDK coloca os anúncios na linha do tempo. Esse processo básico de resolver e carregar publicidades pode causar um atraso inaceitavelmente longo para um usuário que está aguardando para reproduzir seu conteúdo, especialmente se o manifesto contiver vários URLs de publicidade.

**Resolução de anúncios ociosos:**

1. O TVSDK baixa a lista de reprodução.
1. O TVSDK *resolve e carrega* qualquer anúncio precedente, move o player para o status PREPARADO e a reprodução do conteúdo é iniciada.
1. O TVSDK *resolve* cada quebra de anúncio antes de sua posição com base no valor definido em `PTAdMetadata::delayAdLoadingTolerance`.

Por exemplo, por padrão, `delayAdLoadingTolerance` é definido como 5 segundos. Se um AdBreak estiver definido para ser reproduzido às 3:00, ele será resolvido às 2:55:00. Você pode aumentar esse valor se você acredita que a resolução do anúncio levará mais de 5 segundos.

>[!IMPORTANT]
>
>**Fatores a serem considerados com a Resolução de anúncios ociosos:**
>* A resolução de anúncios ociosos só é suportada para fluxos VOD somente com modos de modo SERVER_MAP e de sinalização de anúncios.
>* Por padrão, a Resolução de anúncios ociosos não está ativada. Você deve definir `PTAdMetadata::delayAdLoading` = SIM para habilitá-lo.
>* A resolução de anúncios ociosos é incompatível com o recurso Ativado instantaneamente. Para obter mais informações sobre o Instant On (Ativado instantaneamente), consulte [Instant On (Ativado](../../tvsdk-3x-ios-prog/ios-3x-instant-on-ios.md)instantaneamente).
>* O modo Picture-in-Picture não é compatível com Lazy Ad Resolving. Desative os modos Picture-in-picture se ativar a Resolução de anúncios preguiçosos.
>* A resolução lenta do anúncio não afeta os anúncios precedentes.
>


**Ativar resolução de anúncios ociosos**

Você pode ativar ou desativar o recurso Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçoso (a Resolução de anúncios preguiçosos está desativada por padrão).

Você pode ativar a Resolução de anúncios preguiçosos definindo `PTAdMetadata::delayAdLoading`= SIM ao configurar seus metadados de anúncio.

**APIs relevantes para a resolução de anúncios ociosos:**

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
