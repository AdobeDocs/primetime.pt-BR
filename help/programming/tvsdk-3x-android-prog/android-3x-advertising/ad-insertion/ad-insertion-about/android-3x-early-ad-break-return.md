---
description: Para inserção de anúncios em streaming ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios do break sejam reproduzidos até a conclusão.
title: Implementar um retorno de ad break antecipado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Implementar um retorno de ad break antecipado {#implement-an-early-ad-break-return}

Para inserção de anúncios em streaming ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios do break sejam reproduzidos até a conclusão.

Por exemplo, a duração do ad break em determinados eventos esportivos pode não ser conhecida antes do início do break. O TVSDK fornece uma duração padrão, mas se o jogo for retomado antes da interrupção terminar, o ad break deverá ser encerrado. Outro exemplo é um sinal de emergência durante um ad break em um stream ao vivo.

1. Assinar o `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, e `#EXT-X-CUE`, que são a junção fora/junção em marcadores.
Para obter mais informações sobre como dividir/dividir em marcadores de anúncio, consulte [Geradores de oportunidades e resolvedores de conteúdo](../../ad-insertion/content-resolver/android-3x-content-resolver.md).
1. Usar um personalizado `ContentFactory`.
1. Entrada `retrieveGenerators`, use o `SpliceInPlacementOpportunityGenerator`.

   Por exemplo:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Para obter mais informações sobre o uso de um `ContentFactory`, consulte a etapa 1 em [Implementar um gerador de oportunidades personalizado](../../ad-insertion/content-resolver/android-3x-opp-detector-impl-android.md).

1. No mesmo personalizado `ContentFactory`, implementar `retrieveResolvers` e incluir `AuditudeResolver` e `SpliceInCustomResolver`.

   Por exemplo:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
