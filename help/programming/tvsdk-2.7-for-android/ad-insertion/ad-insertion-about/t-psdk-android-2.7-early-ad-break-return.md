---
description: Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.
seo-description: Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.
seo-title: Implementar um retorno antecipado de anúncios
title: Implementar um retorno antecipado de anúncios
uuid: c67f2158-5df4-458c-a27a-6329c5d26638
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---


# Implementar um retorno antecipado de intervalo de anúncios {#implement-an-early-ad-break-return}

Para a inserção de um anúncio ao vivo, talvez seja necessário sair de uma quebra de anúncio antes que todos os anúncios na quebra sejam reproduzidos até a conclusão.

Por exemplo, a duração do intervalo do anúncio em determinados eventos esportivos pode não ser conhecida antes dos start de pausa. O TVSDK fornece uma duração padrão, mas se o jogo for retomado antes que a pausa termine, a pausa do anúncio deverá ser encerrada. Outro exemplo é um sinal de emergência durante uma pausa de anúncio em uma transmissão ao vivo.

1. Inscreva-se em `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN` e `#EXT-X-CUE`, que são a divisão saída/divisão nos marcadores.

   Para obter mais informações sobre como separar marcadores de anúncios, consulte [Geradores de oportunidade e resolvedores de conteúdo](../../ad-insertion/content-resolver/c-psdk-android-2.7-content-resolver-about.md).

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

1. Na mesma `ContentFactory` personalizada, implemente `retrieveResolvers` e inclua `AuditudeResolver` e `SpliceInCustomResolver`.

   Por exemplo:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```

