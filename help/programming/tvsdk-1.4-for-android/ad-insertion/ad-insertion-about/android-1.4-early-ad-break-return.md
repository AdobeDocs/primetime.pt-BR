---
description: Para inserção de anúncios em streaming ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios do break sejam reproduzidos até a conclusão.
title: Implementar um retorno de ad break antecipado
exl-id: 38386ab7-0e3b-4628-84eb-470d585eb929
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# Implementar um retorno de ad break antecipado {#implement-an-early-ad-break-return}

Para inserção de anúncios em streaming ao vivo, talvez seja necessário sair de um ad break antes que todos os anúncios do break sejam reproduzidos até a conclusão.

Por exemplo, a duração do ad break em determinados eventos esportivos pode não ser conhecida antes do início do break. O TVSDK fornece uma duração padrão, mas se o jogo for retomado antes da interrupção terminar, o ad break deverá ser encerrado. Outro exemplo é um sinal de emergência durante um ad break em um stream ao vivo.

1. Inscreva-se nos marcadores de anúncio de envio/recebimento ( `#EXT-X-CUE-OUT`, `#EXT-X-CUE-IN`, e `#EXT-X-CUE`).

   Para obter mais informações sobre como dividir/dividir em marcadores de anúncio, consulte [Geradores de oportunidades e resolvedores de conteúdo](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-content-resolver-about.md).
1. Usar um personalizado `ContentFactory`.
1. Entrada `retrieveGenerators()`, use o `SpliceInPlacementOpportunityGenerator`.

   Por exemplo:

   ```java
   public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { 
       List<OpportunityGenerator> generators = new ArrayList<OpportunityGenerator>(); 
       generators.add(SpliceInPlacementOpportunityDetector(item)); 
       return generators; 
   }
   ```

   Para obter mais informações sobre o uso de um `ContentFactory`, consulte a etapa 1 em [Implementar um detector de oportunidades personalizado](../../../tvsdk-1.4-for-android/content-resolver/android-1.4-opp-detector-impl.md) .

1. No mesmo personalizado `ContentFactory`, implementar `retrieveResolvers` e incluir `AuditudeResolver` e `SpliceInCustomResolver`.

   Por exemplo:

   ```java
   List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
   contentResolvers.add(new AuditudeResolver(getActivity().getApplicationContext())); 
   contentResolvers.add(new SpliceInCustomResolver()); 
   return contentResolvers;
   ```
