---
description: Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.
seo-description: Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.
seo-title: Implementar um retorno antecipado de anúncios
title: Implementar um retorno antecipado de anúncios
uuid: 0e77414e-86f5-4979-9caa-eaf2f39144a2
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# Implementar um retorno antecipado de anúncios {#implement-an-early-ad-break-return}

Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.

Por exemplo, a duração do intervalo do anúncio em determinados eventos esportivos pode não ser conhecida antes do início do intervalo. O TVSDK fornece uma duração padrão, mas se o jogo for retomado antes que a pausa termine, a pausa do anúncio deverá ser encerrada. Outro exemplo é um sinal de emergência durante uma pausa de anúncio em uma transmissão ao vivo.

1. Assine `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`e `#EXT-X-CUE`, que são a divisão/divisão nos marcadores.
Para obter mais informações sobre como separar marcadores de anúncios, consulte Geradores de [oportunidades e resolvedores](../../ad-insertion/content-resolver/android-3x-content-resolver.md)de conteúdo.
1. Use um personalizado `ContentFactory`.
1. Em `retrieveGenerators`, use o `SpliceInPlacementOpportunityGenerator`.

   Por exemplo:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Para obter mais informações sobre como usar um gerenciador de oportunidade personalizado `ContentFactory`, consulte a etapa 1 em [Implementar um gerador](../../ad-insertion/content-resolver/android-3x-opp-detector-impl-android.md)de oportunidade personalizado.

1. No mesmo personalizado `ContentFactory`, implemente `retrieveResolvers` e inclua `AuditudeResolver` e `SpliceInCustomResolver`.

   Por exemplo:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
