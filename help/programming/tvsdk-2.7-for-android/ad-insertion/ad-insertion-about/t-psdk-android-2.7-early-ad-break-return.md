---
description: Para a inserção de um anúncio em stream ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios no break sejam reproduzidos até o fim.
title: Implementar um retorno de ad break antecipado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 2%

---


# Implementar um retorno antecipado de ad break {#implement-an-early-ad-break-return}

Para a inserção de um anúncio em stream ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios no break sejam reproduzidos até o fim.

Por exemplo, a duração do ad break em determinados eventos esportivos pode não ser conhecida antes do início do break. O TVSDK fornece uma duração padrão, mas se o jogo for retomado antes da conclusão da quebra, o ad break deverá ser encerrado. Outro exemplo é um sinal de emergência durante um ad break em um stream ao vivo.

1. Assine `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` e `#EXT-X-CUE`, que são a divisão/divisão nos marcadores.

   Para obter mais informações sobre como separar marcadores de anúncios/in, consulte [Geradores de oportunidades e resolvedores de conteúdo](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md).

1. Use um `ContentFactory` personalizado.
1. Em `retrieveGenerators`, use o `SpliceInPlacementOpportunityGenerator`.

   Por exemplo:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Para obter mais informações sobre como usar um `ContentFactory` personalizado, consulte a etapa 1 em [Implementar um gerador de oportunidade personalizado](../../ad-insertion/content-resolver/t-psdk-android-2.7-opp-detector-impl-android.md).

1. No mesmo `ContentFactory` personalizado, implemente `retrieveResolvers` e inclua `AuditudeResolver` e `SpliceInCustomResolver`.

   Por exemplo:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

